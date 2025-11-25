1. Imports

Carregam bibliotecas necessárias para:

Acessar DLL (JNA)

Ler entrada do teclado

Ler arquivos

2. Interface ImpressoraDLL

Representa a DLL da impressora.

INSTANCE = Native.load(...) → carrega a DLL.

Cada linha como
int ImpressaoTexto(...);
é uma função da DLL que o Java consegue chamar.

3. Variáveis

conexaoAberta → controla se a impressora está conectada.

tipo, modelo, conexao, parametro → dados da conexão.

scanner → lê o que o usuário digita.

4. capturarEntrada()

Pede um texto ao usuário e retorna a resposta digitada.

5. configurarConexao()

Pede ao usuário:

tipo de conexão

modelo da impressora

porta (ex: COM3)

parâmetro extra
Esses valores ficam guardados para abrir depois.

6. abrirConexao()

Chama a DLL: AbreConexaoImpressora(...)

Se retorno é 0 → conexão aberta com sucesso.

Caso contrário mostra erro.

7. Funções de impressão

Cada uma verifica se a conexão está aberta e então chama a DLL:

ImpressaoTexto() → imprime texto.

ImpressaoQRCode() → imprime QR Code.

ImpressaoCodigoBarras() → imprime código de barras.

AvancaPapel() → avança papel.

AbreGavetaElgin() / AbreGaveta() → abre gaveta.

SinalSonoro() → faz a impressora emitir bips.

imprimeXMLSAT() → imprime arquivo XML SAT.

ImprimeXMLCancelamentoSAT() → imprime XML de cancelamento.

8. Menu do main()

Fica repetindo:

Mostra as opções.

Pergunta qual o usuário quer.

Chama o método correspondente.

Para impressões, também chama Corte(3) depois.

Se opção for 0, fecha e sai.

9. lerArquivoComoString()

Lê um arquivo e devolve o conteúdo como String
