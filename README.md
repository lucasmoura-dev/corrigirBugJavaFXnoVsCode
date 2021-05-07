# Sobre o bug
Ao utilizar o OpenJDK + JavaFX + VSCode, pode retornar os seguintes erros:

Erro #1
```
Error: JavaFX runtime components are missing, and are required to run this application
```

Erro #2
```
Error: Could not find or load main class Libs.javafx-sdk-11.0.2.lib
Caused by: java.lang.ClassNotFoundException: Libs.javafx-sdk-11.0.2.lib
```

# Como corrigir
1. No VSCode, edite o arquivo `launch.json` que está dentro da pasta `.vscode` do seu projeto Java, caso esse arquivo não exista, basta cria-lo em `Run > Add Configuration`.
2. Dentro do arquivo `launch.json`, terá um arquivo semelhante a esse:
```
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Launch Current File",
      "request": "launch",
      "mainClass": "${file}"
    },
    {
      "type": "java",
      "name": "Launch App",
      "request": "launch",
      "mainClass": "App",
      "projectName": "Nome do projeto",
    }
  ]
}
```
3. Basta adicionar o atributo `vmArgs` dentro do segundo objeto do JSON (que contém o atributo `name`de valor 'Launch App'), ficando assim:
`"vmArgs": "--module-path \"<javafx>/lib\" --add-modules javafx.controls,javafx.fxml"`
4. Você deverá substituir `<javafx>/lib` pelo diretório da pasta lib do JavaFX que está no seu computador.
5. Exemplo:
```
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Launch Current File",
      "request": "launch",
      "mainClass": "${file}"
    },
    {
      "type": "java",
      "name": "Launch App",
      "request": "launch",
      "mainClass": "App",
      "projectName": "Nome do projeto",
      "vmArgs": "--module-path \"L:/Java/Java Libs/javafx-sdk-11.0.2/lib\" --add-modules javafx.controls,javafx.fxml"
    }
  ]
}
```
