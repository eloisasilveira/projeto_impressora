# Controle de Impressora Elgin

Projeto de Programação Orientada a Objetos em Java para controlar uma impressora Elgin i8/i9 pelo terminal.

## Integrantes

- Eloisa Silveira — https://github.com/eloisasilveira
- Maria Rita Vicente -
https://github.com/vicenterta
- Sophia Pupim - https://github.com/Sophiapupim

## Requisitos

- Windows.
- Java JDK 21.
- Bibliotecas Elgin e JNA incluídas no projeto.
- Impressora instalada e conectada para utilizar o modo real.

## Como executar

1. Baixe o projeto e extraia a pasta inteira.
2. Abra `executar.cmd`.
3. Entre com o usuário `admin` e a senha `1234`.
4. Confira a configuração da impressora na opção 1.
5. Abra a conexão pela opção 2 antes de imprimir.

O login permite até três tentativas. A configuração inicial é USB, modelo i9. Se o equipamento for i8, altere o modelo antes de abrir a conexão.

No IntelliJ IDEA, abra a pasta do projeto, selecione o JDK 21, adicione `libs Java/jna-5.15.0.jar` às dependências e execute `src/Main.java`. Use a raiz do projeto como diretório de trabalho.

## Menu

| Opção | Função |
| --- | --- |
| 1 | Configurar a conexão |
| 2 | Abrir a conexão |
| 3 | Fechar a conexão |
| 4 | Imprimir texto |
| 5 | Imprimir QR Code |
| 6 | Imprimir código de barras |
| 7 | Imprimir extrato SAT |
| 8 | Imprimir cancelamento SAT |
| 9 | Abrir a gaveta |
| 10 | Emitir um bip curto |
| 11 | Avançar três linhas |
| 12 | Consultar o estado do papel |
| 0 | Sair |

## Funcionamento

- Texto: solicita somente o texto e imprime uma cópia centralizada.
- QR Code: solicita somente o conteúdo; os parâmetros de impressão são fixos.
- Código de barras: imprime um exemplo fixo em CODE128, tipo 8, sem solicitar dados.
- SAT e cancelamento: utilizam os arquivos `XMLSAT.xml` e `CANC_SAT.xml` da pasta do projeto.
- As cinco funções de impressão cortam o papel automaticamente após uma impressão bem-sucedida.
- Gaveta, bip e avanço de papel utilizam parâmetros fixos.
- A configuração aceita USB, serial e rede, com validação de modelo, porta e valores numéricos.
- As operações que dependem da impressora são bloqueadas enquanto a conexão estiver fechada.

## Organização do código

- `Main`: login, menu e execução das opções.
- `Usuario`: conferência do usuário e da senha.
- `Entrada`: leitura e validação das entradas.
- `Impressora`: configuração, conexão e operações da impressora.
- `ImpressoraDLL`: interface de acesso à biblioteca Elgin.
- `AdaptadorElgin`: ligação entre as operações do programa e a DLL.
- `DispositivoImpressora`: interface compartilhada pelo modo real e pela simulação.
- `SimuladorImpressora`: exibição dos comandos sem utilizar uma impressora física.

## Simulação e testes

Abra `simular.cmd` para usar o menu sem uma impressora. O console mostra o texto, os comandos e os cortes solicitados. O QR Code e o código de barras aparecem como dados, e os arquivos XML são exibidos como texto; a simulação não reproduz o formato exato do papel.

Abra `testar.cmd` para executar os testes automatizados de parâmetros, cortes, validação da configuração e tratamento de falhas.

Antes da apresentação, teste a conexão, as impressões, o corte e o bip na impressora da escola. A simulação verifica a lógica do programa, mas não substitui o teste físico.
