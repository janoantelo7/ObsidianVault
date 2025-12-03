---
tags:
  - python/fundamentos
---
# Pip
**Pip** é un gestor de paquetes de python. Os comandos que podemos utilizar en pip son os siguientes:
- **`pip install {package_name}`** : Instalar un paquete.
- **`pip uninstall {package_name}`**: Desinstalar un paquete.
- **`pip install --upgrade package_name`**: Actualizar un paquete.

# Virtualenv
**Virtualenv** é unha ferramenta de python para crear un sandbox de python e así poder separar os paquetes de python dos paquetes do sistema. É bastante recomendable utilizar esto. Os comandos que podemos utilizar para administrar venvs son os siguientes: 

Crear un novo virtual enviroment.
```bash
python3 -m venv <ruta_destino>/<nombre>
```

Activar venv en Linux.
```bash
source <ruta_destino>/<nombre>/bin/activate
```

Activar venv en Windows.
```powershell
.\<ruta_destino>\<nombre>\Scripts\Activate.ps1
```

Desactivar un venv.
```bash
deactivate
```
# Uv 
`uv` é unha ferramenta creada por Astral, escrita en rust para remplazar `pip`, `pip-tools`, `virtualenv` e outros gestores de proxectos de Python.

Para instalalo en Ubuntu executamos o seguinte comando:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Podemos verificar que se instalou correctamente co seguinte comando:
```bash
uv --version
```
## Crear un novo proyecto
A diferencia do antiguo flujo de traballo con `venv` e `pip`, con `uv` podemos gestionar un proyecto enteiro, para eso utilizamos os seguintes comandos:

```bash
mkdir meu_proyecto
cd meu_proyecto
uv init
```

Esto creará un fichero `pyproject.toml` onde se gardan as dependencias e un fichero `hello.py`.

Cando queremos executar o fichero, `uv` crea por nos o entorno virtual ao utilizar o seguinte comando:
```bash
uv run hello.py
```
### Gestión de dependencias
Cando añadimos con `uv` un paquete, este encargase de instalalo e bloquear as versións. A maiores, tamén o añade ao `pyproject.toml`.

```bash
uv add pandas
```

Podemos ver o árbol de dependencias con:
```bash
uv tree
```
## Uso como remplazo de pip
Se queremos traballar co método tradicional tamén o podemos facer xa que `uv` nos proporciona unha interfaz idéntica a `pip` pero máis rápida.

Creamos un entorno virtual:
```bash
uv venv
```

Logo activamos o entorno con:
```bash
source .venv/bin/activate
```

Para instalar paquetes podemos utilizar `uv pip`:
```bash
uv pip install requests numpy
# ou incluso dende un fichero
uv pip install -r requirements.txt
```
## Gestión de versións de Python
Unha das mellores características que ten `uv` é que tamén gestiona as versións de Python sin ter que manejalas con `apt` e interferir na  versión do sistema.

Para instalar unha versión específica de Python:
```bash
uv python install 3.14
```

Podemos executar tamén un script cunha versión específica de Python sin ter que instalala:
```bash
uv run --python 3.11 script.py
```
# Executar ferramentas globales
Se queremos utilizar ferramentas de terminal de Python (como `ruff`), `uv` gestionaas de forma aislada para que non molesten no sistema.

```bash
# Instalar e executar unha ferramenta (por exemplo, ruff)
uv tool install ruff

# Executar una ferramenta sin instalala (efímero)
uv tool run cowsay "Hola mundo!"
```
