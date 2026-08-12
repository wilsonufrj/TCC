# TCC — Biribá

Texto do Trabalho de Conclusão de Curso **“Biribá: Sistema web para a gestão do Programa de Aquisição de Alimentos”**, escrito em LaTeX com o modelo da Escola Politécnica da UFRJ.

O documento principal é `thesis.tex`. A compilação desse arquivo reúne os elementos pré-textuais, os capítulos, as imagens e as referências bibliográficas para gerar `thesis.pdf`.

## Requisitos

É necessário ter uma distribuição LaTeX com `pdflatex`, `bibtex` e `latexmk`.

No Ubuntu ou Debian, instale as ferramentas e os pacotes usados pelo projeto com:

```bash
sudo apt update
sudo apt install latexmk texlive-latex-extra texlive-lang-portuguese texlive-pictures
```

Confirme a instalação:

```bash
latexmk --version
pdflatex --version
bibtex --version
```

## Gerar o PDF

Execute o comando na raiz deste repositório:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error thesis.tex
```

O resultado será criado em:

```text
thesis.pdf
```

O `latexmk` identifica as dependências e executa quantas passagens de `pdflatex` e `bibtex` forem necessárias para atualizar sumário, referências cruzadas e bibliografia.

## Atualização automática durante a escrita

Para manter o compilador ativo e atualizar o PDF sempre que um arquivo LaTeX for salvo, execute:

```bash
latexmk -pdf -pvc -interaction=nonstopmode -halt-on-error thesis.tex
```

Deixe esse terminal aberto enquanto edita o trabalho. Para encerrar o processo, pressione `Ctrl+C`.

Se o ambiente não puder abrir um visualizador de PDF automaticamente, desative essa tentativa e abra `thesis.pdf` manualmente em um leitor com atualização automática:

```bash
latexmk -pdf -pvc -view=none -interaction=nonstopmode -halt-on-error thesis.tex
```

## Compilação manual

Caso `latexmk` não esteja disponível, use esta sequência:

```bash
pdflatex -interaction=nonstopmode -halt-on-error thesis.tex
bibtex thesis
pdflatex -interaction=nonstopmode -halt-on-error thesis.tex
pdflatex -interaction=nonstopmode -halt-on-error thesis.tex
```

As passagens adicionais são necessárias para estabilizar a bibliografia, o sumário, a numeração e as referências internas.

## Limpar arquivos temporários

Para remover somente os arquivos auxiliares e preservar o PDF:

```bash
latexmk -c thesis.tex
```

Depois da limpeza, gere o documento novamente com o comando da seção **Gerar o PDF**.

## Estrutura do projeto

```text
.
├── thesis.tex             # arquivo principal e ordem dos capítulos
├── thesis.bib             # referências bibliográficas
├── poli.cls               # classe LaTeX da Escola Politécnica/UFRJ
├── coppe-unsrt.bst        # estilo bibliográfico usado pelo documento
├── Pre-textual/           # agradecimentos, resumo, abstract e dedicatória
├── Textual/               # capítulos do TCC
├── Pos-textual/           # apêndices
└── Imagens/               # logotipos, diagramas e capturas de tela
```

Para adicionar, remover ou alterar a ordem de capítulos e apêndices, edite os comandos `\include{...}` em `thesis.tex`.

Os arquivos `thesis-expanded.tex` e `thesis.docx`, quando presentes, são versões derivadas. A fonte usada para a geração normal do PDF continua sendo `thesis.tex` e os arquivos incluídos por ele.

## Bibliografia

As referências ficam em `thesis.bib`. O documento usa:

```tex
\bibliographystyle{coppe-unsrt}
\bibliography{thesis}
```

Ao alterar a bibliografia, basta salvar o arquivo se o modo automático estiver ativo ou executar novamente o comando de geração do PDF.

## Solução de problemas

- **Pacote LaTeX não encontrado:** confirme a instalação dos pacotes indicados em **Requisitos**.
- **Imagem não encontrada:** verifique nome, extensão e diferença entre letras maiúsculas e minúsculas no caminho dentro de `Imagens/`.
- **Referência ou citação indefinida:** compile com `latexmk`; uma única execução direta de `pdflatex` normalmente não é suficiente.
- **Erro persistente após uma alteração:** execute `latexmk -c thesis.tex` e compile novamente.
- **PDF não atualiza no visualizador:** reabra `thesis.pdf` em um leitor que detecte mudanças no arquivo ou use a visualização integrada de uma extensão LaTeX do editor.

Arquivos auxiliares e PDFs gerados estão listados no `.gitignore`, evitando que artefatos de compilação sejam incluídos nos commits.
