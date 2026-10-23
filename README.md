# S.A.F.E. para la segunda evaluación

Este proyecto contiene una demostración académica de un agente para consultas de seguridad laboral. El corpus incorpora procedimientos internos simulados y resúmenes externos; no debe usarse para dirigir tareas reales.

## Notebook y ejecución

Abre `Solucion_IA_EV2.ipynb` en Jupyter o Google Colab y ejecuta las celdas desde el inicio. El notebook contiene los 27 registros de demostración y crea su espacio temporal durante la sesión, sin requerir rutas del computador local. En Colab instala los paquetes que falten. Si se informa un conflicto después de instalar dependencias, reinicia el runtime y comienza desde la primera celda.

Se mantiene el modelo `sentence-transformers/paraphrase-multilingual-mpnet-base-v2`, con CPU como alternativa cuando no hay GPU. Si no se instala o descarga el modelo, la búsqueda léxica sirve como respaldo y el cuaderno informa ese modo. Las dependencias principales son `sentence-transformers`, `faiss-cpu`, `langchain`, `langchain-community`, `langchain-openai` y `langgraph`.

La ruta de demostración local funciona sin API. Para activar el agente remoto, agrega `GROQ_API_KEY` en Secrets de Colab o define esa variable de entorno. También se puede leer `API_KEY.txt` si se carga en la sesión o solicitar la clave mediante la entrada oculta del cuaderno. La clave no debe escribirse en una celda ni guardarse en los entregables. La llamada remota no se probó en esta entrega.

## Componentes

- `Solucion_IA_EV2.ipynb`: entorno, datos de demostración, recuperación, herramientas, planificación, memoria, pruebas y limitaciones.
- `safe_agent.py`: demostrador local con búsqueda léxica, derivación prioritaria y memoria breve.
- `knowledge_base.json`: corpus separado para uso local; 22 registros internos y cinco resúmenes externos simulados.
- `langchain_adapter.py`: integración opcional del módulo Python con LangChain y memoria de sesión.
- `agent_architecture.svg`: diagrama de componentes y flujo.

## Resultados y límites de validación

Validación local: respaldo léxico en CPU, 4/4 consultas dirigidas y 4/4 comprobaciones de entorno. Validación real en Colab: runtime Python 3 con GPU T4, modelo multilingüe cargado en CUDA, índice FAISS de 27 fragmentos, 4/4 consultas (incluida abstención fuera de corpus) y 4/4 comprobaciones de entorno. La ejecución no detectó una clave y no llamó al proveedor remoto; esa integración sigue pendiente.

La memoria corta se descarta al reiniciar la sesión. La memoria larga solo se guarda mediante una acción explícita. La traza omite texto literal, pero los hashes y metadatos siguen requiriendo controles de acceso y retención. El prototipo no reemplaza protocolos, capacitación, supervisión ni prevención.
