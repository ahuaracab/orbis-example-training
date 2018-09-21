0.- Verifico el peso inicial git count-objects -v
 

1.-  git verify-pack -v .git/objects/pack/pack-63b5300f60d62b62da641a2538380ba53a0c4216.idx | sort -k 3 -n   | tail -3

Se encuentran los 3 archivos más pesados del proyecto

Luego se copia el hash del archivo más pesado para saber que nombre tiene

2.- git rev-list --objects --all | grep  cfc3322ec593c88d0e4d68c312de3583ca741041 

Una vez que se tiene el nombre "sc.16.tar.gz"

3.- git filter-branch --index-filter 'git rm --cached --ignore-unmatch sc.16.tar.gz' -- --all

Para eliminar el archivo en todos las ramas en las que se vio involucrado

Luego eliminar las referencias y logs de manera forzada y recursiva 

4.- rm -Rf .git/refs/original

5.- rm -Rf .git/logs/

Luego se limpia la basura, es decir archivos que no hacen referencia a ninguna rama

6.- git gc --aggressive --prune=now


7.- Se verifica el peso final del proyecto git count-objects -v