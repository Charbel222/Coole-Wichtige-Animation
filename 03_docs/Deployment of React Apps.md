# Deployment von React-Apps

React ist ein sehr beliebtes JavaScript-Framework für die Entwicklung von Webanwendungen. Wenn es um das Deployment von React-Anwendungen geht, gibt es viele Möglichkeiten und Plattformen, auf denen man sie bereitstellen kann. In diesem Tutorial werden wir uns auf die JAM-Stack-Architektur und serverlose Infrastruktur konzentrieren und GitHub, GitHub Pages und Actions sowie Vercel für die Bereitstellung von React-Anwendungen nutzen.

## JAM-Stack und serverlose Infrastruktur

Der JAM-Stack ist ein moderner Ansatz für die Erstellung von Webanwendungen, der auf JavaScript, APIs und Markup basiert. Im Gegensatz zu herkömmlichen Webanwendungen, bei denen die gesamte Anwendung auf einem Server ausgeführt wird, wird der JAM-Stack verwendet, um eine statische HTML-Seite zu generieren, die dann auf einem CDN (Content Delivery Network) gehostet wird. Diese Seite kann dann mit JavaScript dynamisch gemacht werden, um eine bessere Benutzererfahrung zu bieten.

Die serverlose Infrastruktur ist ein weiteres Konzept, das bei der Bereitstellung von Webanwendungen hilfreich ist. Sie ermöglicht es, Anwendungen zu entwickeln, ohne dass man sich um die Verwaltung von Servern kümmern muss. Die Anwendungen werden in einer Cloud-Infrastruktur ausgeführt und es wird nur für die tatsächlich genutzten Ressourcen bezahlt.

## GitHub, GitHub-Pages und Actions

GitHub ist eine sehr beliebte Plattform für die Versionsverwaltung von Code. Es ist auch ein großartiger Ort, um Ihre React-Anwendung zu hosten. GitHub Pages ist ein kostenloser Hosting-Service von GitHub, mit dem Sie statische Websites hosten können. GitHub Actions ist ein Workflow-Automatisierungstool, mit dem Sie bestimmte Aufgaben automatisieren können, z.B. das automatische Deployment Ihrer React-Anwendung.

Um Ihre React-Anwendung auf GitHub Pages zu hosten, müssen Sie zunächst Ihr Repository auf GitHub erstellen und Ihre Anwendung dort hochladen. Sie können dann die GitHub Pages-Einstellungen verwenden, um Ihre Anwendung zu veröffentlichen. Um das automatische Deployment Ihrer React-Anwendung einzurichten, können Sie GitHub Actions verwenden. Hier ist ein Beispiel-Workflow:

```yaml
# This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm i
    - run: npm run build
    - name: Deploy with gh-pages
      run: |
        git remote set-url origin https://git:${GITHUB_TOKEN}@github.com/${GITHUB_REPOSITORY}.git
        npm run deploy -- -u "github-actions-bot <support+actions@github.com>"
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Dieser Workflow führt die folgenden Schritte aus:

1. Der Code wird ausgecheckt
2. Die Abhängigkeiten werden installiert
3. Die Anwendung wird gebaut
4. Die Anwendung wird auf GitHub Pages veröffentlicht

Um diesen Workflow zu aktivieren, müssen Sie ihn in Ihrem Repository unter ".github/workflows" erstellen.

## Vercel: Architektur, CLI-Setup und Bereitstellung

Vercel ist eine weitere beliebte Plattform für das Deployment von React-Anwendungen. Es ist eine serverlose Plattform, die auf dem JAM-Stack basiert und es Entwicklern ermöglicht, schnell und einfach Anwendungen zu erstellen, zu bereitstellen und zu skalieren. Vercel bietet auch ein kostenloses Starter-Plan, mit dem Sie Ihre Anwendungen schnell bereitstellen können.

### Architektur von Vercel

Die Architektur von Vercel besteht aus einer API, die die Anwendungen erstellt, und einem CDN, der die Anwendungen ausliefert. Wenn Sie Ihre Anwendung auf Vercel bereitstellen, wird Ihre Anwendung in ein Docker-Image verpackt und in der Vercel-Cloud ausgeführt. Vercel verwendet auch intelligente Caching-Strategien, um die Ladezeit Ihrer Anwendungen zu optimieren.

### CLI-Setup für Vercel

Um Ihre Anwendung auf Vercel zu bereitstellen, müssen Sie zunächst die Vercel-CLI installieren. Die Vercel-CLI ist ein Befehlszeilentool, mit dem Sie Ihre Anwendungen schnell und einfach bereitstellen können. Sie können die CLI mit dem folgenden Befehl installieren:

```bash
npm install -g vercel
```

Nach der Installation der Vercel-CLI können Sie Ihre Anwendung mit dem Befehl `vercel` bereitstellen.

### Bereitstellung auf Vercel

Um Ihre Anwendung auf Vercel bereitzustellen, müssen Sie Ihre Anwendung auf GitHub oder GitLab hosten. Wenn Sie Ihre Anwendung auf GitHub oder GitLab hosten, können Sie sie einfach mit Vercel verbinden und automatisch bereitstellen.

Wenn Sie Ihre Anwendung auf Vercel bereitstellen, wird Ihre Anwendung automatisch von Vercel gebaut und auf dem CDN bereitgestellt. Sie können auch verschiedene Einstellungen in der Vercel-Oberfläche vornehmen, um Ihre Anwendung zu konfigurieren, z.B. Umgebungsvariablen, benutzerdefinierte Domains und mehr.

Um Ihre Anwendung auf Vercel zu bereitstellen, können Sie den Befehl `vercel` in der Befehlszeile ausführen. Hier ist ein Beispiel:

```bash
vercel
```

Dieser Befehl wird Ihre Anwendung automatisch auf Vercel bereitstellen. Sie können auch verschiedene Optionen angeben, um Ihre Anwendung zu konfigurieren, z.B. die Umgebungsvariable, die Sie verwenden möchten.