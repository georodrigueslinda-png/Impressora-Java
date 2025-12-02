EXPLICAÇÃO COMPLETA E ORGANIZADA DO CÓDIGO

//Eduarda Oliveira
//Geovanna Rodrigues
//Jessica Caetano
//Matheus Novaes
//Otavio Lima

✅ PASSO A PASSO DO PROJETO — Impressora Java (Elgin / DLL)
1️⃣ Abaixamos o código base do professor

Primeiro pegamos o código base que o professor disponibilizou.
Esse código já tinha a estrutura inicial do programa, como:

menu funcionando

função para abrir/fechar conexão

chamadas básicas da DLL

organização do projeto em Java

Ele serviu como ponto de partida para o nosso sistema.

2️⃣ Baixamos a DLL e os parâmetros no site da Elgin

Depois fomos no site oficial da Elgin (área de desenvolvedores) e baixamos:

E1_Impressora01.dll

documentação das funções

exemplos da Elgin

tabela de parâmetros (modelo, tipo de conexão, porta, etc.)

Esses parâmetros foram usados no nosso código.

3️⃣ Configuramos o Java para usar a DLL

No código, adicionamos as bibliotecas JNA, que permitem que o Java se comunique com DLLs:

import com.sun.jna.Library;
import com.sun.jna.Native;


Isso é necessário porque o Java sozinho não sabe chamar funções externas.

4️⃣ Criamos a Interface da DLL

Depois criamos a interface:

public interface ImpressoraDLL extends Library


Essa interface funciona como uma ponte entre Java e a DLL da Elgin.

Dentro dela colocamos todas as funções que existem na DLL, por exemplo:

AbrirConexaoImpressora

FecharConexaoImpressora

ImprimirTexto

ImprimirQRCode

Corte

AbreGaveta

ImprimeXMLSAT

5️⃣ Carregamos a DLL no Java

Configuramos o caminho:

ImpressoraDLL INSTANCE = (ImpressoraDLL) Native.load(
    "C:\\caminho\\E1_Impressora01.dll",
    ImpressoraDLL.class
);


Isso permite que o Java “abra” a DLL e execute suas funções.

6️⃣ Configuramos as variáveis da conexão

Criamos variáveis globais para armazenar:

tipo da conexão

modelo da impressora

porta (ex: COM3, USB)

parâmetro numérico

estado da conexão (aberta/fechada)

7️⃣ Criamos o Menu Principal

O menu permite o usuário escolher o que deseja fazer:

1 - Configurar Conexão
2 - Abrir Conexão
3 - Imprimir Texto
4 - Imprimir QR Code
5 - Código de Barras
6 - XML SAT
7 - XML Cancelamento
8 - Abrir Gaveta Elgin
9 - Abrir Gaveta
10 - Sinal Sonoro
0 - Fechar e Sair


Cada opção chama uma função da DLL.

8️⃣ Implementamos as Funções de Impressão

Cada função primeiro verifica se a conexão está aberta.
Depois chama a função correspondente da DLL:

imprimir texto

imprimir QR Code

imprimir código de barras

abrir gaveta

sinal sonoro

imprimir XML SAT

cortar papel

9️⃣ Testamos tudo na impressora

Após ajustar todas as funções e caminhos, testamos:

abrir conexão

imprimir texto

QR Code

XML SAT

abrir gaveta

corte

e no final fechar a conexão
