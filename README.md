# 📧 Classificador de Email & Resposta Automática

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)
![LangChain](https://img.shields.io/badge/LangChain-0.3+-orange.svg)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Mixtral-purple.svg)

**Uma aplicação inteligente para classificar emails e gerar respostas automáticas usando IA**

[![Demo](https://img.shields.io/badge/Demo-Live-brightgreen.svg)](https://email-classifier-auto.netlify.app)
[![API](https://img.shields.io/badge/API-Live-blue.svg)](https://email-classifier-back.onrender.com)

</div>

---

## 🎯 Sobre o Projeto

Este projeto é uma aplicação web completa que utiliza inteligência artificial para classificar emails em duas categorias principais: **Produtivo** ou **Improdutivo**, e gera automaticamente sugestões de resposta apropriadas para cada categoria.

### ✨ Funcionalidades Principais

- 🔍 **Classificação Inteligente**: Classifica emails automaticamente como produtivos ou improdutivos
- 🤖 **Resposta Automática**: Gera sugestões de resposta personalizadas baseadas no conteúdo
- 📁 **Upload de Arquivos**: Suporte para arquivos `.txt` e `.pdf`
- 📝 **Entrada de Texto**: Interface para colar texto diretamente
- 🎨 **Interface Moderna**: Design responsivo e intuitivo
- ⚡ **API RESTful**: Backend robusto com FastAPI

### 🏷️ Categorias de Classificação

- **📈 Produtivo**: Emails que requerem ação ou resposta específica
  - Solicitações de suporte técnico
  - Atualizações sobre casos em aberto
  - Dúvidas sobre sistemas
  - Agendamento de reuniões
  - Fechamento de contratos
  - Assuntos empresariais importantes

- **📉 Improdutivo**: Emails que não necessitam ação imediata
  - Mensagens de felicitações
  - Agradecimentos gerais
  - Propagandas e promoções
  - Conteúdo informativo sem ação requerida

---

## 🏗️ Arquitetura do Sistema

```
challenge-autou/
├── 📁 back/                    # Backend (FastAPI)
│   ├── 📄 main.py              # Aplicação principal
│   ├── 📄 llm.py               # Integração com IA (HuggingFace)
│   ├── 📄 requirements.txt     # Dependências Python
│   ├── 📄 client.http          # Testes de API
│   ├── 📁 routes/              # Rotas da API
│   │   └── 📄 email.py         # Endpoint de processamento
│   ├── 📁 utils/               # Utilitários
│   │   └── 📄 nlp.py          # Processamento de texto (NLTK)
│   └── 📁 uploads/            # Arquivos temporários
├── 📄 index.html              # Frontend (HTML/CSS/JS)
├── 📄 styles.css              # Estilos da aplicação
└── 📄 README.md               # Este arquivo
```

### 🔧 Tecnologias Utilizadas

**Backend:**
- **FastAPI**: Framework web moderno e rápido
- **LangChain**: Framework para aplicações com IA
- **HuggingFace**: Modelo Mixtral-8x7B-Instruct para processamento
- **NLTK**: Processamento de linguagem natural
- **PyPDF2**: Extração de texto de PDFs
- **Uvicorn**: Servidor ASGI

**Frontend:**
- **HTML5**: Estrutura semântica
- **CSS3**: Design moderno com variáveis CSS
- **JavaScript**: Interatividade e comunicação com API

**IA/ML:**
- **Mixtral-8x7B-Instruct**: Modelo de linguagem avançado
- **NLTK**: Tokenização, stemming e remoção de stopwords
- **Processamento de Texto**: Limpeza e normalização de dados

---

## 🚀 Instalação e Configuração

### 📋 Pré-requisitos

- Python 3.8 ou superior
- pip (gerenciador de pacotes Python)
- Conta no HuggingFace (para API token)

### 🔑 Configuração da API

1. **Crie uma conta no HuggingFace:**
   - Acesse [huggingface.co](https://huggingface.co)
   - Crie uma conta gratuita
   - Vá para Settings → Access Tokens
   - Crie um novo token com permissões de leitura

2. **Configure as variáveis de ambiente:**
   ```bash
   # Crie um arquivo .env na pasta back/
   echo "HUGGINGFACEHUB_API_TOKEN=seu_token_aqui" > back/.env
   ```

### 🛠️ Instalação do Backend

```bash
# Clone o repositório
git clone <url-do-repositorio>
cd challenge-autou

# Navegue para a pasta do backend
cd back

# Crie um ambiente virtual (recomendado)
python -m venv venv

# Ative o ambiente virtual
# No Windows:
venv\Scripts\activate
# No Linux/Mac:
source venv/bin/activate

# Instale as dependências
pip install -r requirements.txt

# Execute a aplicação
python main.py
```

O servidor estará rodando em `http://localhost:8000`

### 🌐 Instalação do Frontend

O frontend é uma aplicação estática que pode ser servida de qualquer servidor web:

```bash
# Opção 1: Servidor Python simples
cd challenge-autou
python -m http.server 8001

# Opção 2: Live Server (VS Code)
# Instale a extensão "Live Server" e abra index.html

# Opção 3: Qualquer servidor web
# Copie os arquivos index.html e styles.css para seu servidor
```

---

## 📖 Como Usar

### 🖥️ Interface Web

1. **Acesse a aplicação** em `http://localhost:8001` (ou seu servidor)

2. **Escolha uma das opções:**
   - **Upload de arquivo**: Arraste e solte ou clique para selecionar arquivos `.txt` ou `.pdf`
   - **Texto direto**: Cole o conteúdo do email na área de texto

3. **Clique em "Processar Email"**

4. **Visualize os resultados:**
   - Categoria detectada (Produtivo/Improdutivo)
   - Sugestão de resposta automática

### 🔌 API REST

#### Endpoint: `POST /process_email`

**Parâmetros:**
- `text` (opcional): Texto do email como string
- `file` (opcional): Arquivo `.txt` ou `.pdf`

**Exemplo com cURL:**
```bash
curl -X POST "http://localhost:8000/process_email" \
  -F "text=Olá, preciso de ajuda com meu pedido #12345"
```

**Exemplo com arquivo:**
```bash
curl -X POST "http://localhost:8000/process_email" \
  -F "file=@email.txt"
```

**Resposta:**
```json
{
  "category": "PRODUTIVO",
  "suggestion": "Olá! Recebi sua solicitação sobre o pedido #12345. Vou verificar o status e retornar em breve com as informações solicitadas."
}
```

### 🧪 Testando a API

Use o arquivo `client.http` incluído no projeto:

```http
POST http://localhost:8000/process_email HTTP/1.1
Content-Type: multipart/form-data; boundary=boundary123

--boundary123
Content-Disposition: form-data; name="text"

Promoção de pizza.
--boundary123--
```

---

## 🔧 Configurações Avançadas

### 🌡️ Ajustando o Modelo de IA

No arquivo `back/llm.py`, você pode ajustar:

```python
endpoint = HuggingFaceEndpoint(
    repo_id="mistralai/Mixtral-8x7B-Instruct-v0.1",
    task="conversational",
    huggingfacehub_api_token=huggingfacehub_api_token,
    temperature=0.7,  # Ajuste a criatividade (0.0-1.0)
    # max_new_tokens=256,  # Limite de tokens de resposta
)
```

### 🎨 Personalizando o Frontend

**Cores e tema** (`styles.css`):
```css
:root {
  --primary: #5b8cff;      /* Cor principal */
  --accent: #22d3ee;       /* Cor de destaque */
  --success: #22c55e;      /* Verde para produtivo */
  --danger: #ef4444;       /* Vermelho para improdutivo */
}
```

**Endpoint da API** (`index.html`):
```javascript
// Para desenvolvimento local:
const endpoint = 'http://localhost:8000/process_email';

// Para produção:
const endpoint = 'https://email-classifier-back.onrender.com/process_email';
```

---

## 🚀 Deploy

### ☁️ Deploy do Backend (Render)

1. **Conecte seu repositório ao Render**
2. **Configure as variáveis de ambiente:**
   - `HUGGINGFACEHUB_API_TOKEN`: Seu token do HuggingFace
3. **Configure o build:**
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `python main.py`

### 🌐 Deploy do Frontend (Netlify)

1. **Conecte seu repositório ao Netlify**
2. **Configure o build:**
   - Build Command: (deixe vazio)
   - Publish Directory: `/` (raiz do projeto)
3. **Atualize o endpoint da API** no `index.html`

---

## 🧪 Exemplos de Uso

### 📧 Email Produtivo
```
Assunto: Problema com sistema de pagamento

Olá equipe,

Estou enfrentando dificuldades para processar pagamentos através do sistema. 
O erro aparece quando tento finalizar uma compra. Podem me ajudar?

Atenciosamente,
João Silva
```

**Resultado esperado:**
- Categoria: **PRODUTIVO**
- Sugestão: "Olá João! Recebi sua mensagem sobre o problema no sistema de pagamento. Nossa equipe técnica irá investigar e retornar em breve com uma solução."

### 📧 Email Improdutivo
```
Assunto: Obrigado!

Olá pessoal,

Só queria agradecer pelo excelente atendimento de vocês!

Abraços,
Maria
```

**Resultado esperado:**
- Categoria: **IMPRODUTIVO**
- Sugestão: "Obrigado!"

---

## 🐛 Solução de Problemas

### ❌ Erro: "Missing HUGGINGFACEHUB_API_TOKEN"
**Solução:** Verifique se o arquivo `.env` existe na pasta `back/` e contém o token correto.

### ❌ Erro: "Formato de arquivo não permitido"
**Solução:** Use apenas arquivos `.txt` ou `.pdf`. Verifique a extensão do arquivo.

### ❌ Erro: "Arquivo muito grande"
**Solução:** O limite é de 10MB. Reduza o tamanho do arquivo ou use a opção de texto.

### ❌ Frontend não conecta com o backend
**Solução:** 
1. Verifique se o backend está rodando em `http://localhost:8000`
2. Confirme se o endpoint no `index.html` está correto
3. Verifique as configurações de CORS no `main.py`

---

## 🤝 Contribuindo

1. **Fork** o projeto
2. **Crie** uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. **Commit** suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. **Push** para a branch (`git push origin feature/AmazingFeature`)
5. **Abra** um Pull Request

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

---

## 👨‍💻 Autor

**Israel Alvares**
- GitHub: [@Cr-Israel](https://github.com/Cr-Israel)
- LinkedIn: [Carlos Israel](https://www.linkedin.com/in/carlos-israel-64460a227/)

---

## 🙏 Agradecimentos

- [HuggingFace](https://huggingface.co) pela plataforma de IA
- [FastAPI](https://fastapi.tiangolo.com) pelo framework web
- [LangChain](https://langchain.com) pela integração com IA
- [NLTK](https://www.nltk.org) pelo processamento de linguagem natural

---

<div align="center">

**⭐ Se este projeto foi útil para você, considere dar uma estrela! ⭐**

</div>
