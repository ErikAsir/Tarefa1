1. Descargar e comprobar que unha imaxe está no teu equipo

- Pra descargar unha imaxe no equipo temos ir a terminar e executar o seguinte comando:

docker pull ubuntu

- agora imos verificar que a imaxe este no equipo 

docker images 

2. Crear un contenedor sen nome, queda arrincado?, cómo obtés o nome?

- Podemos crear un contenedor sen nombre usando a imaxe de ubuntu

docker run -d ubuntu sleep 1000

· -d: Executa o contenedor en segundo plano
· sleep 1000: Manten o contenedor activo por 1000 segundos

¿ Queda arrincado ? 

- Podemos comprobalo con:

docker ps

- Co comando anterior deveriamos de ver un contenedor en execución cun nombre asinado autimáticamente  

¿ Como obtemos o seu nome ?

- Ao executar docker ps, veremos unha columna chamada NAMES. O nome do contenedor aparecerá ahí

3. Crea un contenedor coo nome 'u1', cómo accedes a el?

- Podemos crear un contenedor e asinarle o nome u1 usando:

docker run -dit --name u1 ubuntu

· dit: Crea un contenedor en modo interactivo 
· --name u1: asina o nome u1 ao contenedor 

¿ Cómo accedes a el ?

- Pra acceder ao contenedor e executar comandos dentro del usamos o seguinte comando:

docker exec -it u1 bash

- Isto te abrirá unha sesión de terminal dentro do contenedor u1

4. Comproba a súa ip e fai ping a google.com

- Pra obter a IP dun contenedor empregaremos o seguinte comando:

docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAdress}}{{end}}' u1

- Isto dara a dirección IP do contenedor

Ping a google.com

- O primerio seria acceder ao contenedor 

docker exec -it u1 bash

- Dentro do contenedor executaremos 

ping google.com

5. Crea un contenedor coo nome 'bono', pódes facer ping entre os contenedores?

- Comezamos por crear o contenedor bono:

docker run -dit --name bono ubuntu

- Pra facer ping entren os contenedores u1 e bono, necesitamos obter a IP do contenedor bono:

docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'bono

- Logo, accedemos ao contenedor u1 e facemos ping a IP de bono:

docker exec -it u1 bash 
ping IP_de_bono

- Isto permitira comprobar se poden comunicarse

6. Se pechas as terminales, qué pasa coo contenedor?

- Se cerras as terminales donde tes un contenedor en execución no modo interactivo o contenedor parará. Pero se o contenedor esta executandose no modo detached (-d), seguirá funcionando incluso se pechas o terminal

7. Cánta memoria no disco duro ocupaches? usa docker para calculalo

- Pra ver canto espacio ocupa no disco as imaxes , contenedores, volumenes e caché podemos excutar:

docker system df

8. Cánta RAM ocupan os contenedores? Crea varios para calculalo

Podemos ver o uso da RAM dos contenedores en tempo real co seguinte comando:

docker stats 

9. Cómo fixeches para clonar o repositorio

- O primeiro que fixe e crear un novo repositorio no git, clonalo e engadirlle un archivo readme2.

git clone https://github.com/ErikAsir/Tarefa1.git

10. Cómo engades o arquivo readme2.md

- Comeze creando o archivo  readme2.md e logo pra añadilo utilicei o comando git add e por utimo pra gardar os cambios no repositorio utilicei git commit -m.

touch readme2.md
git add readme2.md
git commit -m "Archivo readme tarefa 2"

11. Os pasos a seguir para subir o arquivo que estás editando e o arquivo readme2.md

- Primeiro aseguramos que hemos agreado ambos archivos

git add readme.md readme2.md

- Logo realizamos un commit pra gardar os cambios 

git commit -m 

- Por ultimo subimos os cambios a o repositorio remoto

git push origin main

12. Cómo comprobarías que existen diferencias entre o teu repositorio local e o remote.

Pra comprobar se existen diferenzas entre o repositorio local e remoto podese usar o seguinte comando:

git fetch

- O comando anterior actualizara o teu repositorio local co os cambios do remoto sen fusionalos. Logo se pode ver as diferenzas con este comando:

git diff origin/main

