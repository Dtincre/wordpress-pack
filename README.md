# wordpress-pack (instalación de paquetes al clonar)

IMPORTANTE: Git no ejecuta scripts automáticamente al hacer `git clone`. Esto es una medida de seguridad.
Para instalar los paquetes (apache2, php y mariadb) después de clonar, usa una de las siguientes opciones:

1) Método recomendado (manual y seguro)
   git clone https://github.com/Dtincre/wordpress-pack.git
   cd wordpress-pack
   ./install.sh        # te pedirá confirmación
   # o para no interactuar:
   ./install.sh -y

2) Activar hooks del repo (semi-automático)
   git clone https://github.com/Dtincre/wordpress-pack.git
   cd wordpress-pack
   # Habilita los hooks incluidos en .githooks (recomendado en lugar de copiar al .git/hooks)
   ./install-hooks.sh
   # A partir de aquí, ciertas operaciones (post-checkout) ejecutarán scripts del repo.

   Nota: los hooks no se habilitan automáticamente por seguridad; el usuario debe ejecutar el comando anterior.

3) Usar Docker (entorno aislado y reproducible)
   docker build -t wordpress-pack-dev .
   docker run -it wordpress-pack-dev bash

4) Ejecutar (BAJO TU RESPONSABILIDAD) una línea remota:
   # No recomendado en general, pero es una opción para usuarios que confían en el repo:
   git clone https://github.com/Dtincre/wordpress-pack.git && cd wordpress-pack && curl -sSL https://raw.githubusercontent.com/Dtincre/wordpress-pack/main/install.sh | sudo bash -s -- -y

El repositorio incluye:
- install.sh          : script para instalar paquetes en Debian/Ubuntu.
- .githooks/post-checkout : hook de ejemplo que puede ejecutar install.sh una vez que habilites hooks.
- install-hooks.sh    : script para configurar core.hooksPath a .githooks.
- Dockerfile          : imagen Debian con los paquetes instalados.
```
