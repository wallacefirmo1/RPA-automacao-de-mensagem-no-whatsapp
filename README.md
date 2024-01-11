# Automatizando o Marketing no WhatsApp com Python: Um Guia Prático de RPA

Este script Python automatiza o envio de mensagens no WhatsApp para uma lista de contatos. Ele usa as bibliotecas `openpyxl`, `urllib.parse`, `webbrowser`, `time` e `pyautogui`.

## Dependências

- Python 3
- openpyxl
- urllib
- webbrowser
- time
- pyautogui

## Como usar

1. Instale as dependências listadas acima.
2. Crie um arquivo Excel chamado `clientes.xlsx` com uma planilha chamada `Sheet1`. A primeira coluna deve conter os nomes dos clientes e a segunda coluna deve conter os números de telefone dos clientes.
3. Execute o script Python.

## O que o script faz

Para cada linha na planilha (começando na segunda linha), o script faz o seguinte:

1. Lê o nome e o número de telefone do cliente.
2. Abre o WhatsApp Web no navegador padrão com uma nova mensagem para o número de telefone do cliente.
3. Espera 25 segundos para permitir que o WhatsApp Web seja carregado e o QR Code seja escaneado.
4. Digita uma mensagem personalizada para o cliente e pressiona enter para enviar.
5. Espera 7 segundos e envia mensagens adicionais.
6. Clica no sinal de + para anexar um arquivo.
7. Navega pelo menu para selecionar um arquivo de áudio.
8. Confirma e envia o arquivo de áudio.
9. Fecha a janela do navegador.

## Ajustes

Você pode precisar ajustar os tempos de espera (`sleep`) e as coordenadas do clique (`pyautogui.click`) dependendo da velocidade do seu computador e da resolução da sua tela.

## Código

Aqui está o código completo:

```python
import openpyxl
from urllib.parse import quote
import webbrowser
from time import sleep
import pyautogui

workbook = openpyxl.load_workbook('clientes.xlsx')
pagina_clientes = workbook['Sheet1']

for linha in pagina_clientes.iter_rows(min_row=2, max_col=2):
    nome = linha[0].value
    telefone = linha[1].value
    link_mensagem_whatsapp = f'https://web.whatsapp.com/send?phone={telefone}'
    webbrowser.open(link_mensagem_whatsapp)
    sleep(25)  # Ajuste este tempo conforme necessário
    pyautogui.typewrite(f'OE aí {nome}, Wallace na área!')
    pyautogui.press('enter')
    sleep(7)
    
    # Envio de mensagens adicionais e operações na interface
    pyautogui.typewrite('Vou te mandar um audio...', 0.1)
    sleep(7)
    pyautogui.hotkey('enter')
    sleep(5)
    pyautogui.typewrite('Assim que ouvir me responde aqui.', 0.1)
    sleep(3)
    pyautogui.hotkey('enter')
    sleep(5)

    # Clicar no sinal de +
    pyautogui.click(x=553, y=705)
    sleep(3)
        
    # Clicar no Fotos e Video
    pyautogui.click(x=618, y=359)
    sleep(3)
        
    # Clicar em Opcao
    pyautogui.click(x=331, y=542)
    sleep(3)
        
    # Clicar em Personalizado
    pyautogui.click(x=658, y=499)
    sleep(3)
        
    # Clicar em Todos arquivos
    pyautogui.click(x=674, y=520)
    sleep(3)
        
    # Localizar e Selecionar o audio de envio
    audio = pyautogui.hotkey('1')
    sleep(3)
        
    # Confirmar o audio a ser envido Enviar
    pyautogui.hotkey('enter')
    sleep(3)
        
    # Enviar o audio
    pyautogui.hotkey('enter')
    sleep(3)
        
    pyautogui.hotkey("command", "w")
    sleep(3)
