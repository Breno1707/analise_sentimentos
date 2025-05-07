# 📚 Resumo e Insights: Labs AI-900 (Text Analysis & Speech)

## Lab 6: Text Analysis (Análise de Texto)

### 🔎 Objetivo

Aprender a usar o **Azure Cognitive Services** para analisar textos de forma automatizada.

### 🛠️ Atividades Principais

* Criar um recurso de **Text Analytics** no Azure.
* Usar a API para:
    * **Detectar idioma** do texto.
    * **Analisar sentimentos** (positivo, neutro, negativo).
    * **Reconhecer entidades** (pessoas, lugares, organizações).
    * **Extração de frases-chave**.

### 💡 Insights

* **Automação de insights**: O serviço permite que empresas analisem automaticamente grandes volumes de texto de redes sociais, reviews e e-mails.
* **Multilíngue**: Suporta múltiplos idiomas, o que é crucial para empresas globais.
* **Facilidade com REST APIs e SDKs**: Permite integração simples com apps em Python, C#, JavaScript e outros.
* Excelente para **chatbots, CRM e monitoramento de marca**.

## Lab 9: Speech (Serviços de Fala)

### 🔎 Objetivo

Explorar os serviços de **fala** do Azure para converter entre fala e texto e criar apps mais acessíveis.

### 🛠️ Atividades Principais

* Criar um recurso de **Speech** no Azure.
* Testar:
    * **Conversão de fala para texto** (Speech to Text).
    * **Conversão de texto para fala** (Text to Speech).
    * **Reconhecimento de locutor** (identificar quem está falando).
    * **Tradução de fala** em tempo real.

### 💡 Insights

* **Inclusão e acessibilidade**: Permite criar apps mais acessíveis para pessoas com deficiência.
* **Aplicações práticas**:
    * **Legendagem automática** em vídeos.
    * **Assistentes virtuais** que entendem e falam com o usuário.
    * **Tradução simultânea** em eventos globais.
* **Personalização**: É possível treinar modelos personalizados de voz para adaptar à marca da empresa.
* Fator chave na criação de **experiências omnichannel** (voz, texto, chat, etc.).

## 🚀 Conexão Entre os Dois Labs

* Ambos fazem parte dos **Azure Cognitive Services** e podem ser combinados para criar soluções como:
    * Chatbots que entendem texto e também a fala do usuário.
    * Ferramentas de análise que **escutam** ligações telefônicas, **transcrevem** e depois **analisam o sentimento** e as entidades.

## ✅ Dicas para Aplicação Real

* Se está se preparando para uma **entrevista técnica** ou uma **prova de certificação AI-900**, foque em entender **quando usar cada serviço** e os **casos de uso reais**.
* Pratique usando o **Azure Portal** e também com pequenos scripts em **Python** ou **C#** para chamar essas APIs.

# 🚀 Projeto Completo: Speech ➡️ Text ➡️ Análise com Azure + Python

## 🎯 Pré-Requisitos
- Conta no [Azure Portal](https://portal.azure.com/)
- Recursos criados:
  - **Azure Speech** (para fala)
  - **Azure Text Analytics** (para texto)
- Bibliotecas Python instaladas:

```bash
pip install azure-ai-textanalytics azure-cognitiveservices-speech
```

---

## 🗂️ Código Completo: Speech ➡️ Texto ➡️ Análise de Sentimento

```python
# 📚 Importar as bibliotecas
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential
import azure.cognitiveservices.speech as speechsdk

# 🔐 Informações do Azure (substitua pelas suas)
speech_key = "<SUA-CHAVE-SPEECH>"
speech_region = "<SUA-REGIÃO-SPEECH>"
text_key = "<SUA-CHAVE-TEXT>"
text_endpoint = "https://<SEU-ENDPOINT-TEXT>.cognitiveservices.azure.com/"

# 🔊 Função para converter fala para texto
def speech_to_text():
    speech_config = speechsdk.SpeechConfig(subscription=speech_key, region=speech_region)
    recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config)

    print("🎙️ Fale algo para analisarmos...")
    result = recognizer.recognize_once()

    if result.reason == speechsdk.ResultReason.RecognizedSpeech:
        print(f"📝 Texto reconhecido: {result.text}")
        return result.text
    else:
        print("❌ Não foi possível reconhecer a fala.")
        return None

# 🧠 Função para analisar o texto com Text Analytics
def analyze_text(text):
    client = TextAnalyticsClient(endpoint=text_endpoint, credential=AzureKeyCredential(text_key))

    documents = [text]

    # Detectar idioma
    language_result = client.detect_language(documents=documents)[0]
    print(f"🌐 Idioma detectado: {language_result.primary_language.name}")

    # Analisar sentimento
    sentiment_result = client.analyze_sentiment(documents=documents)[0]
    print(f"❤️ Sentimento: {sentiment_result.sentiment.capitalize()}")

# 🚀 Executar o fluxo completo
def main():
    text = speech_to_text()
    if text:
        analyze_text(text)

# ▶️ Rodar
if __name__ == "__main__":
    main()
```

---

## ✅ Resultado Esperado

1. O programa vai pedir para você **falar** algo.
2. Ele converte sua fala para **texto**.
3. Depois, ele analisa:
   - O **idioma** detectado.
   - O **sentimento** do texto (Positivo, Neutro ou Negativo).

### Exemplo:
```
🎙️ Fale algo para analisarmos...
📝 Texto reconhecido: I love using Azure services!
🌐 Idioma detectado: English
❤️ Sentimento: Positive
```

---

## 💡 Dicas para Expansão
- Adicione a **extração de entidades** no `analyze_text()`.
- Use a API de **tradução de fala** para suportar múltiplos idiomas.
- Grave todo o fluxo em um **arquivo de log** para análise posterior.

---

## 🏆 Conclusão
Agora você tem um mini-sistema que:
- **Escuta** sua voz
- **Transcreve**
- **Analisa sentimentos**
  
Ótimo exercício para a certificação **AI-900** e para projetos reais com **Azure Cognitive Services** 🚀
