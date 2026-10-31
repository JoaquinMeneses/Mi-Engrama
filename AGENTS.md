## Reglas de Arquitectura del Vault  
1. Cada tema dentro de `3. Recursos/` contiene dos subcarpetas: 
- `Fuentes/`: Archivos brutos e inmutables aportados por el usuario. 
- `Sintesis/`: Tu capa Wiki. Aquí debes crear y mantener los conceptos (`[[nota]]`), el `index.md` del tema y el `log.md`. 
2. Al ingerir un nuevo archivo en `3. Recursos/[Tema]/Fuentes/`, genera las páginas de síntesis dentro de `3. Recursos/[Tema]/Sintesis/`. 
3. Mantén los enlaces bidireccionales `[[nota]]` conectados entre conceptos de la carpeta Síntesis.