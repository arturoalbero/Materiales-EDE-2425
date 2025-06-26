
# Github pages


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Github pages](#github-pages)
  - [Introducción a GitHub Pages](#introducción-a-github-pages)
  - [Cómo crear y publicar un sitio con GitHub Pages](#cómo-crear-y-publicar-un-sitio-con-github-pages)
    - [1. Crear un repositorio en GitHub](#1-crear-un-repositorio-en-github)
    - [2. Agregar los archivos del sitio](#2-agregar-los-archivos-del-sitio)
    - [3. Activar GitHub Pages](#3-activar-github-pages)
    - [4. Actualizar el sitio](#4-actualizar-el-sitio)
- [Consideraciones adicionales](#consideraciones-adicionales)
- [Recursos adicionales](#recursos-adicionales)

<!-- /code_chunk_output -->




## Introducción a GitHub Pages

[GitHub Pages](https://pages.github.com/) es un servicio gratuito de GitHub que permite alojar sitios web directamente desde un repositorio. Es especialmente útil para sitios personales, documentación de proyectos, portafolios y proyectos estáticos. Los sitios alojados pueden usar HTML, CSS, JavaScript u otros generadores estáticos como Jekyll.

Documentación oficial:
[https://docs.github.com/en/pages](https://docs.github.com/en/pages)

## Cómo crear y publicar un sitio con GitHub Pages

### 1. Crear un repositorio en GitHub

1. Inicia sesión en [github.com](https://github.com).
2. Haz clic en el botón "New" o "New repository".
3. Asigna un nombre al repositorio (por ejemplo, `mi-sitio`).
4. Puedes marcar la opción "Add a README file" si lo deseas.
5. Haz clic en "Create repository".

### 2. Agregar los archivos del sitio

Sube tus archivos HTML, CSS y otros necesarios al repositorio. Puedes hacerlo de dos formas:

**Opción A**: Usando la interfaz web

* Entra al repositorio.
* Haz clic en "Add file" > "Upload files".
* Sube los archivos y haz commit.

**Opción B**: Usando Git localmente
Si prefieres usar la terminal:

```bash
git clone https://github.com/tu-usuario/mi-sitio.git
cd mi-sitio
# Agrega tus archivos
git add .
git commit -m "Sitio inicial"
git push origin main
```

Github pages también **admite archivos en formato markdown**, que son traducidos por el framework Jekyll a HTML.

### 3. Activar GitHub Pages

1. Ve al repositorio en GitHub.
2. Haz clic en la pestaña "Settings".
3. En el menú lateral, busca "Pages" (en la sección "Code and automation").
4. En la sección "Source", selecciona la rama (`main` o `master`).
5. Luego elige la carpeta raíz (`/root`) o `/docs` si tu contenido está en esa carpeta.
6. Haz clic en "Save".

GitHub generará una URL para tu sitio, algo como:

```
https://tu-usuario.github.io/mi-sitio/
```

Puede tardar unos segundos en estar disponible.

### 4. Actualizar el sitio

Cada vez que hagas un nuevo *commit* y *push* a la rama configurada, GitHub Pages actualizará automáticamente el sitio.

# Consideraciones adicionales

* El sitio debe ser estático. GitHub Pages no ejecuta código del lado del servidor (como PHP).
* Si deseas usar un generador estático como Jekyll, GitHub Pages lo soporta de forma nativa.
* También puedes usar un dominio personalizado.


# Recursos adicionales

* Guía completa de GitHub Pages:
  [https://docs.github.com/en/pages](https://docs.github.com/en/pages)

* Personalizar sitios con Jekyll:
  [https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll)

> **Actividad**
> Crea una página web estática en github pages. Usa archivos markdown para generar contenido, así como HTML, CSS y Javascript. Documenta el proceso.
