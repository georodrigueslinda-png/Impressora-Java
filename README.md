EXPLICAÇÃO COMPLETA E ORGANIZADA DO CÓDIGO

//Eduarda Oliveira
//Geovanna Rodrigues
//Jessica Caetano
//Matheus Novaes
//Otavio Lima

✅ 1. IMPORTAÇÕES (Imports)

São as bibliotecas que o programa usa.
Biblioteca JNA (acesso à DLL)
import com.sun.jna.Library;
import com.sun.jna.Native;
Permitem que o Java chame funções que estão dentro da DLL da impressora.
Entrada de dados
import java.util.Scanner;
Usado para ler o que o usuário digita no menu.

Arquivos
import javax.swing.JFileChooser;
import java.io.File;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.io.FileInputStream;


Usadas para ler arquivos XML (embora apenas um método realmente use isso).

✅ 2. INTERFACE DA DLL (ImpressoraDLL)
public interface ImpressoraDLL extends Library

Define uma “ponte” entre Java e a DLL.

Carrega a DLL
ImpressoraDLL INSTANCE = (ImpressoraDLL) Native.load(
        "C:\\caminho\\E1_Impressora01.dll",
        ImpressoraDLL.class
);

Isso faz o Java “abrir” a DLL e permitir chamar suas funções.
Funções da DLL
A interface declara todas as funções que existem dentro da DLL:
Abrir conexão
Fechar conexão
Imprimir texto
Imprimir código de barras
Imprimir QR Code
Cortar pape
Abrir gaveta
Fazer bip (sinal sonoro)
Imprimir XML do SAT
Imprimir XML de cancelamento
Cada método retorna int:
0 = sucesso
outro número = erro

✅ 3. VARIÁVEIS DO PROGRAMA
private static boolean conexaoAberta = false;
private static int tipo;
private static String modelo;
private static String conexao;
private static int parametro;
Servem para guardar:
tipo de conexão
modelo da impressor
porta COM/USB
parâmetro da DLL
estado da conexão (aberta ou não)
Scanner para ler entradas:
private static final Scanner scanner = new Scanner(System.in);

✅ 4. capturarEntrada()

Função básica para ler e retornar texto digitado pelo usuário.

✅ 5. configurarConexao()
Pede ao usuário:
Tipo da conexão (USB/Serial/etc.)
Modelo da impressora
Porta (COM3, USB, etc.)
Parâmetro extra
Guarda tudo nas variáveis do programa.
Se a conexão já estiver aberta, ela não deixa reconfigurar.

✅ 6. abrirConexao()
Chama a função da DLL:
AbreConexaoImpressora(tipo, modelo, conexao, parametro)
Se retornar 0 → conexão aberta
Senão → mostra código de erro
Também ativa:
conexaoAberta = true;

✅ 7. fecharConexao()
 
verificar se a conexão está aberta
chamar FechaConexaoImpressora()
conferir retorno
fechar e alterar conexaoAberta para false

✅ 8. FUNÇÕES DE IMPRESSÃO

Cada função verifica se a conexão está aberta.
Se não estiver, mostra aviso.
ImpressaoTexto()
Imprime "Teste de impressao".
ImpressaoQRCode()
Imprime um QR Code.
ImpressaoCodigoBarras()
Imprime código de barras tipo 8.
AvancaPapel()
Avança 2 linhas.
AbreGavetaElgin() / AbreGaveta()
Comandos para abrir a gaveta da impressora.
SinalSonoro()
Faz a impressora emitir beeps.

✅ 9. IMPRESSÃO DE XML DO SAT

Usa dois arquivos:
XML normal
ImprimeXMLSAT("path=C:\\...\\XMLSAT.xml", 0)
XML de cancelamento
Mesmo esquema, mas com uma assinatura QRCode extra.

✅ 10. MENU PRINCIPAL (main)

O main cria um loop com um menu:

1 - Configurar Conexão
2 - Abrir Conexão
3 - Imprimir Texto
4 - Imprimir QR Code
5 - Código de Barras
6 - XML SAT
7 - XML Cancelamento SAT
8 - Abrir Gaveta Elgin
9 - Abrir Gaveta
10 - Sinal Sonoro
0 - Fechar Conexão e Sair


Cada opção chama a função correspondente.
Após impressões, chama:
Corte(3)
para cortar o papel.
Quando o usuário digita 0:
chama fecharConexao()
encerra o loop
fecha o scanner

✅ 11. lerArquivoComoString()

Lê um arquivo e retorna seu conteúdo como uma String.
Serve para abrir archivos XML, TXT, etc.

(No seu código atual, está lá mas não está sendo usado.)
