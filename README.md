# telar-modulos

El catálogo oficial de módulos de [telar](https://github.com/nicorivas/telar): lo que se mergea aquí, lo revisó
quien mantiene telar, y sale **revisado** en la página de cada telar (⚙ → módulos → disponibles).

```sh
telar modulos catalogo           # lo que hay
telar modulos instalar grafo     # uno, en la versión que dice el catálogo
```

## El archivo

Uno solo: [`.telar/catalogo.toml`](.telar/catalogo.toml). Es el mismo formato que un equipo usa en su propio
repositorio para su catálogo (también `.telar/catalogo.toml`). Está descrito en
[docs/modulos.md](https://github.com/nicorivas/telar/blob/main/docs/modulos.md) de telar.

Cada entrada apunta a una **etiqueta o un commit** de su repositorio, nunca a una rama: lo que se instala es lo que se
revisó. Y dice lo que el módulo pide fuera de su carpeta (`[permisos]`), igual que su `modulo.toml`.

## Sumar o actualizar un módulo

Desde la carpeta del módulo:

```sh
telar modulos revisar .                             # lo que le falta
telar modulos publicar . --version v0.1.0 --seco    # la entrada, para verla
telar modulos publicar . --version v0.1.0           # etiqueta, sube y abre el PR aquí
```

O, con un agente: la skill `/modulos` (la pone `telar agente instalar`).

El PR lo revisa una acción (`.github/workflows/revisar.yml`): baja cada módulo en su versión y comprueba que su
manifiesto se lea, que traiga `[permisos]` y que lo que el catálogo dice que pide sea lo que pide. Después lo lee
una persona: qué corre al instalarse (`[instalar]`), qué pide, y si hace lo que dice.

## Lo que no entra

- Un módulo sin `[permisos]`, o que pide más de lo que necesita.
- Uno que apunta a una rama.
- Uno que se llama como una orden de telar.
