# 📘 Guía Básica de Git

---

## 🔧 Instalación y configuración

```bash
git --version     # vemos versión de git si lo tenemos instalado
```
El -- es para pedir algo completo, en este caso toda la versión.

```bash
git help          # ayuda con comandos
git help 'comando' # más info sobre un comando específico
```

```bash
git config --global user.name "Tu nombre"
git config --global user.email "tumail@gmail.com"
```
```bash
git config --global -e
```

```bash
git config --global -e
```
Chequeamos el usuario y email.
Tocando 'A' modificamos datos, salimos con ESC :wq! y si queremos salir sin guardar: :q!. (notar que escribo : -> :qw! o :q!)

## 🚀 Inicializar repositorio
```bash
git init                     # inicializa el repositorio
git config --global init.defaultBranch <name>  # rama por defecto
#recomendable git config --global init.defaultBranch main
Ctrl+L                       # limpiamos consola
```
### 📄 Manejo de archivos y commits

```bash
git status        # info de commits, rama actual
git add <archivo> # agregamos archivo para commitear
git add .         # agregamos todos los archivos
git reset <archivo> # lo removemos del stage
```
```bash
git commit -m "Primer commit"   # hacemos un commit
git log                         # vemos commits anteriores
```
```bash
git checkout -- .  # volvemos atrás en el proyecto (último commit)
```
### 🌿 Ramas
```bash
git branch                  # vemos en qué rama estamos
git branch -m master main  # renombrar rama de master a main
```
⚠️ SI BORRAS LA CARPETA OCULTA .git BORRAS TU REPOSITORIO

## ⚠️ Problemas con CRLF

```bash
$ git add -A
warning: LF will be replaced by CRLF in historia/batman.historia.md.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in historia/superman.historia.md.
The file will have its original line endings in your working directory.
```
SOLUCION
```bash
git config core.autocrlf true
```
### 📝 Combinaciones y atajos

```bash
git commit -am "Readme Actualizado"
```
Este comando hace el commit y el git add . combinados SOLO SI el archivo ya fue commiteado al menos una vez.

Si es un archivo nuevo, primero se debe hacer:
```bash
git add .
```
### 🧠 Info del git log
git log muestra:

```bash
commit <código hash> HEAD -> main
```
HEAD es el último commit e indica a dónde apunta.
Salir con :q
### 📂 Agregar archivos de a poco al stage
A veces el git add . añade de mas, y es buena practica "modularizar" los commits, es decir si trabajo con A y con B, hacer commits de B por un lado y de A por otro, no commitear ambas cosas a la vez, asi podemos hacerlo

```bash
git add *.HTML ## Todos los .html
git add js/*.js ## Todos los .js de la carpeta js
git add CSS/ ## Toda la carpeta CSS
```
A carpetas vacías git no las guarda, por eso se usa un .gitkeep ya que suele ser importante tener algunas carpetas aunque esten vacias

```bash
git add uploads/.gitkeep
```
### 🔍 Atajos y alias útiles
Algunos comandos de git son muy largos o incluso las respuesta de algunos comandos, como el log, pueden ser muy largas, aca unas pares de config que ayudan a ver el stage mas facil y logs mas cortitos

```bash
git status --short
git config --global alias.s status --short
# o si falla:
git config --global alias.s "status --short"
```
Ahora con ``` git s ``` ves un status mas simple y de manera mas rapida.

```bash
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
```
Ahora con ``` git lg ``` ves un log mas simple.

### 🔄 Comparar cambios

```bash
git diff             # ver cambios sin haber hecho git add
git diff --staged    # ver cambios en el stage, listos para el commit
```

### ✏️ Corregir último commit
```bash
git commit --amend -m "Nuevo mensaje"
```
### 🧹 Resetear commits

```bash
git reset --soft HEAD^
```
Elimina el último commit pero no los cambios.


```bash
git reset --hard HEAD^
```
Elimina el último commit y sus cambios.

#### ¿CAMBIOS?
con cambios me refiero a todo lo que codeaste, ejemplo COMMIT A32 -> BC4 -> FG8* 
Estamos en el FG8 pero justo,,,, algo esta mal PERO no tan mal, si queremos volver al commit BC4 pero sin perder TODO el codigo del commit FG8 que queremos borrar (xq capaz nos dimos cuenta q agregamos un archivo que no queremos tener en ese commit con ese mensaje etc etc etc) hacemos el SOFT, en cambio si todo lo que codeamos en un desastre commiteamos para que github nos ponga el cuadradito verde pero nada funciona y antes si, ahi se usaria el HARD porque nos vuelve al commit y al codigo del BC4. 
#### ⚠️ ESTO HACERLO UNICAMENTE EN CASOS MUY EXTREMOS | ⚠️ reset usar solo si es muy muy necesario

### ⚠️ Notas sobre HEAD y el reset
HEAD apunta al último commit de la rama actual (en checkout).

Se puede reemplazar HEAD por el hash del commit.

^ indica a partir de ese commit cuántos borrar:

HEAD^ borra el último

HEAD^3 borra ese y dos más anteriores
```bash
git reset --hard HEAD^
git reset --hard HEAD^3
```
### Subir tus commits de git a GitHub
Si no clonaste y arrancaste todo desde git, create un repo en GitHub con el nombre que quieras ej ```turepo```
y se supone que en git ya hiciste un ```git init``` ```git add . (yo recien hice git add comandos.md)``` 
Y lo que sigue es esto
```bash
git remote add origin https://github.com/turepo.git # Le indicamos a que repo de GitHub les pertenece nuestro repo de Git
git push -u origin main #(en este caso mi rama es el main)
```
Despues pusheamos normalmente sin volver a hacer el git remote add origin :)