1 - Escreva um script que exibe uma ajuda sobre redirecionadores. Para cada redirecionador estudado ( >, >>, 2>, 2>>, &>, &>>, <, <<, <<<, e |) o script deve imprimir o redirecionador, uma explicação sobre o seu funcionamento e um exemplo útil de uso. (Use suas próprias palavras, evite apenas copiar de alguma fonte O.0).

    > redirecionadores.sh
    chmod +x redirecionadores.sh
    vim redirecionadores.sh
        
        #!/bin/bash
        
        echo -e "Explicação de redirecionadores: \n"
        
        echo -e "O redirecionador > redireciona a saída para um arquivo, se o arquivo existir, ele apaga o arquvo e cria novamente\n"
        echo -e "O redirecionador >>  redireciona a saída para um arquivo, insere o conteúdo no final, caso o arquivo não exista, ele cria\n"
        echo -e "O redirecionador 2>  redireciona a saída de erro para um arquivo, se o arquivo existir, ele apaga o arquivo e cria novamente\n"
        echo -e "O redirecionador 2>>  redireciona a saída de erro para um arquivo, insere o conteúdo no final, caso o arquivo não exista, ele cria\n"
        echo -e "O redirecionador &>  redireciona a saída padrão e de erro para um arquivo, se o arquivo existir, ele apaga o arquivo e cria novamente\n"
        echo -e "O redirecionador &>>  redireciona a saída padrão e de erro para um arquivo, insere o conteúdo no final, caso o arquivo não exista, ele cria\n"
        echo -e "O redirecionador < redireciona um arquivo já existente como entrada\n"
        echo -e "O redirecionador << permite que você digite um arquivo que substituirá a entrada, no qual será preciso passar um nome para que o mesmo seja digitado para o encerramento da digitação\n"
        echo -e "O redirecionador <<< permiete que você redirecione uma string digitada após o redirecionamento como entrada\n"
        echo -e "O redirecionador | redireciona a saída do comando anterior para o comando seguinte ao mesmo"
        
        
2 - Escreva um script que receba 3 nomes de arquivos passados como argumentos de linha de comando. Use o comando ls usando estes arquivos como argumentos. Redirecione todos os erros para o arquivo erro.log e todas as saídas corretas para o arquivo ok.log.

      > ex2.sh
    chmod +x ex2.sh
    vim ex2.sh
        
        #!/bin/bash
        
        a="$1"
        b="$2"
        c="$3"
        
        ls ${a} >> ok.log 2>> erro.log
        ls ${b} >> ok.log 2>> erro.log
        ls ${c} >> ok.log 2>> erro.log
        
        
3 - Escreva um script que peça para o usuário digitar 2 números inteiros. Imprima o menor e o maior dos dois. Use o formato abaixo.

      > ex3.sh
    chmod +x ex3.sh
    vim ex3.sh
        
        #!/bin/bash
        
        a="$1"
        b="$2"
        
        if (( a > b )); then
            echo "Menor: ${b}"
            echo "Maior: ${a}"
        else
            echo "Menor: ${a}"
            echo "Maior: ${b}"
        fi
        
        
4 - Escreva um script que receba três nomes de diretórios como parâmetros de linha de comando e, usando exatamente uma linha de comando para cada diretório e operadores condicionais (&& ou ||) imprima SIM caso o diretório exista ou uma frase criativa, caso contrário.

        > ex4.sh
    chmod +x ex4.sh
    vim ex4.sh
        
        #!/bin/bash
        
        a="$1"
        b="$2"
        c="$3"
        
        [ -f ${a} ] && echo "SIM" || echo "O arquivo nao e digno para existir"
        [ -f ${b} ] && echo "SIM" || echo "O arquivo nao e digno para existir"
        [ -f ${c} ] && echo "SIM" || echo "O arquivo nao e digno para existir"
        
        
5 - Escreva um script que peça para o usuário digitar 4 nomes de arquivos e imprima o nome daquele que possui o maior número de linhas. Caso algum arquivo não exista, imprima erro: o arquivo ‘<nome_do_arquivo>’ não existe, e saia do script.

        > ex5.sh
        chmod +x ex5.sh
        vim ex5.sh
        
        #!/bin/bash
        
        read -p "Digite o nome de 4 arquivos: " a b c d
        
        if [ ! -e ${a} ];then
            echo "O arquivo ${a} não existe"
            exit 1
        fi
        
         if [ ! -e ${b} ];then
            echo "O arquivo ${b} não existe"
            exit 1
        fi
        
         if [ ! -e ${c} ];then
            echo "O arquivo ${c} não existe"
            exit 1
        fi
        
         if [ ! -e ${d} ];then
            echo "O arquivo ${d} não existe"
            exit 1
        fi
        
        primeiro=$(cat ${a} | wc -l)
        segundo=$(cat ${b} | wc -l)
        terceiro=$(cat ${c} | wc -l)
        quarto=$(cat ${d} | wc -l)
        
        maior=${primeiro}
        result=${a}
        
        if (( $segundo > $maior ));then
            result=${b}
            maior=${segundo}
        fi
        
        if (( $terceiro > $maior ));then
            result=${c}
            maior=${terceiro}
        fi
        
        if (( $quarto > $maior ));then
            result=${d}
            maior=${quarto}

        fi
        
        echo ${result}
        echo ${maior}
        
        
6 - Escreva um script que recebe o nome de um arquivo como argumento de linha de comando e imprime BAD caso este arquivo não exista ou possua mais que 3 linhas. Caso contrário, exiba o nome do arquivo e a última linha do mesmo.

        > ex6.sh
        chmod +x ex6.sh
        vim ex6.sh
        
        #!/bin/bash

        a="$1"
        linhas=$(cat ${a} | wc -l)
        
        if [ ! -e ${a} ]; then
            echo "BAD"
        elif (( $linhas > 3 )); then
            echo "BAD"
            
        else
            echo "Nome do arquivo: ${a}"
            echo $(tail -n1 ${a})
            
7 - Escreva um script que peça para o usuário digitar 4 números COM CASAS DECIMAIS. Imprima o menor deles. Use o bc.

        
        > ex7.sh
        chmod +x ex7.sh
        vim ex7.sh
        
