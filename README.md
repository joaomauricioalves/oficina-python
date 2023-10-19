<h1>Olha o que eu posso fazer com Python!</h1>

<p>Python é uma linguagem de programação de alto nível, interpretada e orientada a objetos, criada em 1991 por Guido van Rossum. Sua sintaxe é conhecida por sua simplicidade e clareza, tornando-a uma das tecnologias mais procuradas, tanto no Stack Overflow quanto em requisitos de empregos.</p>

<p>Para mais informações, confira a pesquisa do Stack Overflow sobre as <a href="https://survey.stackoverflow.co/2023/#technology-most-popular-technologies">tecnologias mais populares</a>.</p>

<p>Quando pensamos em simplicidade, não percebemos todo o poder que o Python oferece. Não subestime essa linguagem, pois você pode utilizá-la para:</p>

<ul>
  <li><b>Inteligência artificial</b></li>
  <li><b>Ciência de dados</b></li>
  <li><b>Computação gráfica</b></li>
  <li><b>Big Data</b></li>
  <li><b>Desenvolvimento web</b></li>
  <li><b>Testes automatizados</b></li>
  <li><b>Scripting e automação</b></li>
  <li>e muito mais!</li>
</ul>

<p><b>Vale ressaltar que os exemplos apresentados têm fins acadêmicos. Não encorajamos o uso para atividades ilegais ou antiéticas. A responsabilidade pelo uso do conhecimento adquirido aqui é de cada leitor.</b></p>

<p>Nesta oficina, abordaremos apenas alguns exemplos práticos. Você provavelmente já se deparou com situações em que precisava encontrar soluções, mas estavam em sites duvidosos ou com programas questionáveis. No entanto, com scripts em Python, muitas dessas questões podem ser resolvidas em poucas linhas de código.</p>

<p>Todos os exemplos nesta oficina foram desenvolvidos usando o Google Colab.</p>

<h2>Exemplo 1 -GTTS</h2>

<p><b>gTTS (Google Text-to-Speech)</b> é uma biblioteca Python que usa a API do Google Translate para poder narrar textos.</p>

<p>Com um novo notebook aberto, vamos escrever o primeiro trecho do código.</p>

<p>O primeiro passo é instalar no ambiente temporário criado no google colab.</p>

```
#Instalando a biblioteca gtts

!pip install gtts

```

<p>O próximo passo </p>

```
from gtts import gTTS

vamosTodos = 'Vasco da Gama, a sua fama assim se fez!'

gtts = gTTS(vamosTodos, lang='pt')
gtts.save('vasco.ogg')
```
<p> Um exemplo simples que pode ser aperfeiçoado para outros fins :D</p>

<p> O arquivo "vasco.ogg" é salvo no diretório padrão chamado content.</p>

<h2>Exemplo 2 - Extrair áudio de vídeo online</h2>

<p>Novamente, a responsabilidade recai sobre você em relação ao uso deste código ;)</p>

<p>Além disso, lembre-se de que as bibliotecas frequentemente se tornam obsoletas, o que pode prejudicar seu funcionamento. Portanto, é importante verificar se há atualizações disponíveis e fazer testes antes de usá-las.</p>

<p>Imagine que um autor tenha postado no YouTube um vídeo com exemplos de efeitos sonoros e que eles estão sob a licença Creative Commons. Você deseja extrair apenas o áudio. Como você pode fazer isso com Python?</p>


<p> No Google Colab faremos o uso da biblioteca <b>yt_dlp</b></p>

<p><b>yt_dlp</b> é uma biblioteca python que também tem um programa CLI para realizar downloads de vídeos e áudios no YouTube.</p>

```
# Instalando a biblioteca
!pip install yt_dlp

```
<p>Após isso, temos:</p>

```
import yt_dlp

link = input("Digite o link do vídeo do YouTube a ser baixado: ")

ydl_opts = {
    'format': 'bestaudio/best',
    'outtmpl': '/content/%(title)s.%(ext)s',
    'postprocessors': [{
        'key': 'FFmpegExtractAudio',
        'preferredcodec': 'mp3',
        'preferredquality': '320',
    }],
}
with yt_dlp.YoutubeDL(ydl_opts) as ydl:
    ydl.download([link])
```

<p> Link para teste </p>

```
https://youtu.be/dPZTh2NKTm4?si=BSBNqW1K1oRR3f5t

```
<h2>Exemplo 3 - Importar PDF e recuperar seu Texto</h2>

<p>Imagine que você quer manipular um texto escrito em um arquivo.pdf e quero que um script me retorne o texto do pdf <b>pypdf2</b></p>

<p>No Google Colab você vai precisar instalar:</p>

```

!pip install pypdf2

```
<p>O próximo passo é habilitar o upload de arquivos no Google Colab:</p>
<p><b>Sugiro renomear para teste.pdf</b></p>

```

from google.colab import files  #biblioteca para fazer upload
uploaded = files.upload()

```
<p>Esse arquivo será salvo no diretório "/content" do Google Colab</p>

```
import PyPDF2

# pdfFileObj = o arquivo pdf sendo lido de forma binária
pdfFileObj = open('/content/teste.pdf', 'rb')

# cria-se uma forma de ler esse objeto binário
pdfReader = PyPDF2.PdfReader(pdfFileObj)

# A página é especificada do objeto de leitura
pageObj = pdfReader.pages[0]

# com o método extract_text() remove somente o texto do objeto binário na página selecionada.
text = pageObj.extract_text()

# Feche o arquivo PDF após a extração do texto
pdfFileObj.close()

print('-' * 20)
print(text)

```

<p>O resultado pode está no terminal!</p>

<h2>Exemplo 4 - Importar PDF e Salvar DOCX</h2>

<p>Mudando pouca coisa dos outros códigos</p>

```

import PyPDF2
from docx import Document


pdfFileObj = open('/content/teste2.pdf', 'rb')
pdfReader = PyPDF2.PdfReader(pdfFileObj)
#chama o método Document() para criar um documento word
doc = Document()

# Usando uma estrutura de repetição ele extrai o texto de um objetoPDF e adiciona o texto ao documento word
for pageObj in pdfReader.pages:
    text = pageObj.extract_text()
    doc.add_paragraph(text)

# Salva o documento DOCX em um arquivo
doc.save('/content/saida.docx')

pdfFileObj.close()

```
<h2>Exemplo 5 - OCR de texto em imagem </h2>

<p> 1º Passo – Instalar as seguintes bibliotecas:</p>

```

!pip install pymupdf pytesseract Pillow

```


<p> 2º Passo – Usar esse código para fazer um Upload </p>
<p>Enviar um PDF com imagem para a máquina virtual do <b>Google Colab</b>.</p>

```

from google.colab import files  #biblioteca para fazer upload
uploaded = files.upload()
```



<p>3º Passo – Instalar na máquina virtual linux do <b>Google Colab</b> bibliotecas vindas do repositório através de apt-get</p>

```

!apt-get install -y tesseract-ocr
!apt-get install -y libtesseract-dev

```



<p>4º Passo – Rodar esse código</p>

```
import io
import fitz  # PyMuPDF
from PIL import Image
import pytesseract

#criando uma função para mostrar o texto do pdf
def pdf_to_text(pdf_path):
    text = ""
    doc = fitz.open(pdf_path)

    for page_num in range(doc.page_count):
        page = doc[page_num]
        image_list = page.get_images(full=True)

        for img_index, img in enumerate(image_list):
            xref = img[0]
            base_image = doc.extract_image(xref)
            image_bytes = base_image["image"]
            image = Image.open(io.BytesIO(image_bytes))

            # Realiza OCR na imagem
            text += ocr_image(image) + "\n"

    return text
#Função que realiza o OCR
def ocr_image(image):
    # Realiza OCR na imagem
    text = pytesseract.image_to_string(image)
    return text


pdf_path = '/content/pdf.pdf'
result = pdf_to_text(pdf_path)
print(result)
```


<h2>Exemplo 6 - Webscaping</h2>

<p>O Webscaping, também chamado de raspagem de dados, envolve um aspecto sensível, pois pode haver riscos de infringir os direitos de propriedade de conteúdos criados por outras pessoas. Portanto, a coleta de informações de sites de terceiros é uma responsabilidade exclusiva sua.</p>
<p>O conteúdo apresentado aqui tem o propósito de ser educacional e acadêmico. Portanto, utilize o conhecimento obtido com responsabilidade e cautela.</p>


<p>Existem no mínimo duas formas de uma pessoa normalmente coletar informações de um site de notícias.</p>
<ul>
    <li>Selecionando com o mouse a informação desejada</li>
    <li>Inspecionando o código HTML e copiando da TAG</li>
</ul>
<p>O que o código abaixo fará será
<ul>
    <li>Realizar uma requisição http (protocolo usado para páginas web) usando <b>requests</b></li>
    <li>Com outra biblioteca chamada BeautifulSoup ela analisará o HTML e com isso extraímos o dado desejado </li>
</ul>

<p>Vejamos:</p>

<p>Instalando as bibliotecas necessárias</p>

```
!pip install requests
!pip install BeautifulSoup4

```

<p>Em seguida temos:</p>

```
import requests
from bs4 import BeautifulSoup
```

<p>Para as requisições HTTP, usaremos a função:</p>

```
def fazerRequests(url):
  resposta = requests.get(url)
  resposta.encoding = resposta.apparent_encoding
  soup = BeautifulSoup(resposta.text, 'html.parser')
  return soup
```
<p>Veja que essa função retorna um objeto tipo soup</p>
<p>O objeto tipo soup é necessário para o manipular o BeautifulSoup4, onde dele podemos extrair várias informações da página analisada</p>
<p>Nesse sentido vamos criar uma função para extrair o título</p>

```
def tituloVascoNoticias(soup):
title = soup.title.getText()
return title
```
<p>Também será criada uma função para extrair outras informações</p>

```
def pegarInfoVascoNoticias(soup):

    info = soup.find_all('a', class_='loop__item__link')

    mensagem = []
    i =1
    while i < 6:
        mensagem.append(info[i].get_text())
        i += 1
    delimiter = '. \r\n'
    mensagem = delimiter.join(mensagem)
    mensagem = mensagem.replace(". ", ". <br/>")
    return mensagem

```
<p>Nessa função foi coletada a informação da tag "a" na class ="loop__item__link", pois nela é onde encontramos a notícia, contudo em outras páginas, tanto a tag, como a classe podem ser diferentes.</p>
<p>Poderia ser uma tag &lt;p&gt;&lt;/p&gt;, &lt;span&gt;&lt;/span&gt; ou outra qualquer com outra classe ou id do CSS.</p>
<p>Outro ponto a destacar é que o tratamento de delimitadores e a limpeza desses dados são de acordo com cada página envolvida.</p>

<p>Agora vamos aplica isso ao método main da seguinte forma:</p>

```
def main():
    vasco = "https://www.vasconoticias.com.br"
    titulo = tituloVascoNoticias(fazerRequests(vasco))
    noticia = pegarInfoVascoNoticias(fazerRequests(vasco))
    print(titulo)
    print(noticia)

if __name__ == '__main__':
    main()

```

<p>Agora vejamos as notícias quentinhas sobre o Vasco da Gama!</p>
