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
        
        #!/bin/bash
        
        read -p "Digite quatro números com casas decimais: " a b c d
        
        x=$(bc <<< "${a} < ${b}")
        
        if (( ${x} == 1 ));then
            menor=${a}
        else
            menor=${b}
        fi
        
        z=$(bc <<< "${c} < ${menor}")
        
        if (( ${z} == 1 ));then
            menor=${c}
        fi
        
        y=$(bc <<< "${d} < ${menor}")
        
        if (( ${y} == 1 ));then
            menor=${d}
        fi
        
        echo "Menor: $menor"
        
        
8 - Escreva um script que imprima todos os números ímpares entre 0 e 108. Melhore o script para que imprima todos os números ímpares entre a e b, sendo a o primeiro parâmetro de linha de comando, enquanto que b é o segundo.

    -primeira forma
        
        > ex8.sh
        chmod +x ex8.sh
        vim ex8.sh
        
        #!/bin/bash
        
        for (( i=1; i<109; i+=2 ));do
             echo ${i}
        done
        
    -melhorado
        #!/bin/bash
        
        a="$1"
        B="$2"
        
        for (( i=${a}; i<(( ${b} + 1 )); i++ ));do
            
            x=$(( ${i}%2 ))
            
            if (( ${x} != 0 ));then
                echo ${i}
            fi
        done
        
        
9 - Escreva um script que peça para o usuário digitar dois números, a e b, e calcule (e exiba na tela) a soma de todos os números de a até b, sem incluir a e b.

        > ex9.sh
        chmod +x ex9.sh
        vim ex9.sh
        
        #!/bin/bash
        
        read -p "Digite dois números: " a b
        soma=0
        for (( i=(( ${a} + 1 )); i<${b}; i++ ));do
            soma=$(( $soma + ${i} ))
        done
        
        echo "Soma: $soma"
        
10 - Escreva um script que receba vários nomes de arquivo como parâmetros de linha de comando (o número de parâmetros pode variar de execução para execução) e imprima o nome de cada arquivo passado seguido de SIM, caso o arquivo exista, e de NAO caso contrário. Caso todos os arquivos passados existam, o script deve exibir uma mensagem criativa.

        
        > ex10.sh
        chmod +x ex10.sh
        vim ex10.sh
        
        #!/bin/bash
        
        
        for x in ${*};do
            if [ -e ${x} ];then echo "${x} SIM"
            else
                a=$(( $a + 1 ))
                echo "${x} NAO"
            fi
       done        
        if (( $a == 0 ));then
            echo "Framengo is the better"
        fi
        
11 - Escreva um script chamado 11.sh. Este deve receber um ou mais parâmetros de linha de comando. Se um destes parâmetros for “logica”, o script deve imprimir uma ajuda sobre os parâmetros lógicos do comando test. Se um destes parâmetros for “aritmetica”, o script deve imprimir uma ajuda sobre os parâmetros aritméticos do comando test. Se um destes parâmetros for “strings”, o script deve imprimir uma ajuda sobre os parâmetros para strings do comando test. Se um destes parâmetros for “variáveis”, o script deve imprimir uma ajuda sobre os parâmetros para variáveis do comando test. Se um destes parâmetros for “arquivos”, o script deve imprimir uma ajuda sobre os parâmetros sobre arquivos do comando test.

        > 11.sh
        chmod +x 11.sh
        vim 11.sh
        
        #!/bin/bash        
        
        for x in ${*};do
            if [ ${x} == "arquivo" ];then
                echo "Ajuda sobre o comando test"
                echo "Opções para testes de arquivo"
                echo "test -d <arq>: verdadeiro se o arquivo é um diretorio"
                echo "test -e <arq>: verdadeiro se o arquivo existe"
                echo "test -f <arq>: verdadeiro se é um arquivo comum, caso não, retorna falha"
            fi
            
            if [ ${x} == "aritmetica" ];then
                echo "Ajuda sobre o comando test"
                echo "Opções para testes de aritmetica"
                echo "test <int1> -ge <int2>: verdadeiro se o int1 é maior ou igual ao int2"
                echo "test <int1> -eq <int2>: verdadeiro se o int1 é igual ao int2"
                echo "test <int1> -gt <int2>: verdadeiro se o int1 é maior que int2"
                echo "test <int1> -le <int2>: verdadeiro se o int1 é menor ou igual ao int2"
                echo "test <int1> -lt <int2>: verdadeiro se o int1 é menor que int2"
                echo "test <int1> -ne <int2>: verdadeiro se o int1 é não é igual ao int2"
            fi
            
            if [ ${x} == "strings" ];then
                echo "Ajuda sobre o comando test"
                echo "Opções para testes de strings"
                echo "test <str1> = <str2>: Verdadeiro se a str1 é igual a str2"
                echo "test <str1> != <str2>: Verdadeiro se a str1 é diferente da str2"
                echo "test <str1> > <str2>: Verdadeiro se a str1 é maior que str2"
                echo "test <str1> < <str2>: Verdadeiro se a str1 é menor que str2"
            fi
            
             if [ ${x} == "variaveis" ];then
                echo "Ajuda sobre o comando test"
                echo "Opções para testes de variaveis"
                echo "test -z <variavel>: verdadeiro se a variavel for vazia"
                echo "test -n <variavel>: verdadeiro se a variavel não for vazia"
             fi
            
            if [ ${x} == "logica" ];then
                echo "Ajuda sobre o comando test"
                echo "Opções para testes de logica"
                echo "test <agr> -a <agr>: -a serve como um AND(e) lógico"
                echo "test <agr> -o <agr>: -a serve como um OR(ou) lógico"            
            fi
        done

12 - Escreva um script que imprima a palavra DIRS e abaixo liste todos os diretórios da pasta atual. Em seguida imprima a palavra FILES e abaixo liste todos os arquivos (sem diretórios ou links) da pasta atual. Por fim, imprima a palavra LINKS e abaixo liste todos os links simbólicos da pasta atual. Use for, if e o comando test (pode ser a versão curta: [ ]).

        > ex12.sh
        chmod +x ex12.sh
        vim ex12.sh
        
        #!/bin/bash
        
        dire=$(echo $(ls -d */))
        
        echo "DIRS--------------"
        
        for x in ${dire};do
            echo ${x}
        done
        
        files=$(echo $(ls -F | grep -v '/$'))
        
        echo "FILES-----------"
        
        for z in ${files};do
            echo ${z}
        done
        
        links=$(echo $(ls -la | grep ^l))
        
        echo "LINKS-----------------"
        
        echo $links
            
