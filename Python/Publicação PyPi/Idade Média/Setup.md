
Para criação do pacote precisamos primeiro realizar o setup a partir da biblioteca setuptools dentro de um arquivo setup.py

```
from setuptools import setup

setup (
	name = ("meu_pacote"),
	packages = ["meu_pacote")],
	install_requires=["pandas"], #Quando tem depedências
)
```