# Estrutura dos Artigos sobre 12 Fatores

Este documento explica a organização dos arquivos de documentação e artigos no repositório.

## 📄 Arquivos e seus Propósitos

### 📖 README.md
**Propósito:** Documentação principal do repositório no GitHub  
**Formato:** Síntese estruturada dos 12 Fatores  
**Características:**
- Tom profissional e direto
- Cada fator com citação, explicação "Na prática", benefícios e exemplos
- Seção sobre como os fatores se conectam
- Guia "Por onde começar"
- CTA para contribuição no repositório
- Ideal para quem busca referência rápida e prática

---

### 📝 MEDIUM_PT-BR.md
**Propósito:** Artigo para publicação no Medium (português)  
**Formato:** Narrativa fluida e envolvente  
**Características:**
- Começa com exemplo prático de bug de produção
- Tom mais literário e storytelling
- Contextualização histórica (2011 → 2026)
- Explicação dos fatores de forma mais narrativa
- Ideal para leitura linear e engajamento
- ~8-10 minutos de leitura

---

### 📝 MEDIUM_EN.md
**Propósito:** Artigo para publicação no Medium (inglês)  
**Formato:** Tradução completa do artigo PT-BR  
**Características:**
- Mantém a mesma estrutura narrativa
- Adaptações culturais e de estilo quando necessário
- Exemplos traduzidos e contextualizados
- Mesma experiência de leitura da versão PT

---

### 🗂️ README_OLD.md
**Propósito:** Backup do README anterior  
**Status:** Arquivo de referência histórica  
**Pode ser removido** após confirmação de que o novo README está adequado

---

## 🎯 Quando Usar Cada Um

| Contexto | Arquivo |
|----------|---------|
| Documentação do repositório GitHub | `README.md` |
| Publicar artigo no Medium (PT) | `MEDIUM_PT-BR.md` |
| Publicar artigo no Medium (EN) | `MEDIUM_EN.md` |
| Referência rápida dos 12 fatores | `README.md` |
| Artigo para blog/LinkedIn | `MEDIUM_PT-BR.md` ou `MEDIUM_EN.md` |

---

## 📋 Diferenças de Estilo

### README.md (Síntese Estruturada)
```markdown
## 1. Base de Código (Codebase)

> **Uma única base de código com controle de versão, múltiplos deploys.**

Manter o código centralizado...

**Na prática:** Todos os ambientes compartilham...

**Benefícios:**
- Facilita integração contínua
- Rollback simples
```

### MEDIUM_PT-BR.md (Narrativa Fluida)
```markdown
## 1. Base de código

Cada aplicação tem uma única base de código, versionada, 
e essa base gera muitos deploys.

Desenvolvimento, homologação e produção compartilham o mesmo 
repositório. O que muda entre eles é a configuração...
```

---

## ✅ Checklist de Publicação

### Para o Medium:
- [ ] Copiar conteúdo de `MEDIUM_PT-BR.md` ou `MEDIUM_EN.md`
- [ ] Colar no editor do Medium
- [ ] Adicionar imagem de capa (sugestão: diagrama dos 12 fatores)
- [ ] Revisar formatação (títulos, listas, código)
- [ ] Adicionar tags sugeridas no final do arquivo
- [ ] Incluir link para o repositório GitHub

### Para o GitHub:
- [ ] `README.md` está atualizado
- [ ] Links internos funcionam (Codebase/README.md, etc.)
- [ ] Licença está mencionada
- [ ] Links para 12factor.net estão corretos

---

**Última atualização:** Novembro 2026
