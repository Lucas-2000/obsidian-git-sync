**Criar o ambiente virtual Linux/Windows**

```
## Windows
python -m venv .venv
source .venv/Scripts/activate # Ativar ambiente

## Linux 
## Caso não tenha virtualenv. "pip install virtualenv"
virtualenv .venv
source .venv/bin/activate # Ativar ambiente
```

**Instalar os seguintes pacotes Iniciais.**

```
pip install django
pip install pillow
```

**Para criar o arquivo _requirements.txt_**

```
pip freeze > requirements.txt
```
