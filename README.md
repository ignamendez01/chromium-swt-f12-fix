# chromium-swt-f12-fix
Este repositorio contiene mi solución al issue relacionado con habilitar la apertura de DevTools presionando F12 cuando el navegador Chromium embebido tiene foco.

# Contexto del problema
En la implementación actual de Equo Chromium para SWT, presionar F12 no abría DevTools.
El objetivo era lograr que si el navegador tiene foco y el usuario presiona F12, se abra DevTools automáticamente como sucede en un navegador host real, y además:
+ Solo habilitarlo cuando -Dchromium.debug=true
+ Permitir sobrescribir con -Dchromium.devtools_shortcut=true|false

# Qué hice
Modifiqué únicamente la clase:

com.equo.chromium.swt.internal.Chromium

Agregando un listener de teclas que:
+ Intercepta F12
+ Verifica:
  + Si chromium.debug está en true
  + Y si chromium.devtools_shortcut NO está definido o está en true
+ Llama a extraApi.getBrowser().openDevTools()
