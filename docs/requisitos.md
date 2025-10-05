# Requisitos do Projeto — Brechó App

## 1. Objetivo
Desenvolver uma aplicação web para gestão e divulgação de um brechó, permitindo cadastrar peças, exibir catálogo e controlar estoque.

## 2. Problema
Pequenos brechós têm dificuldade em manter estoque organizado e catálogo atualizado para clientes, reduzindo alcance e vendas.

## 3. Escopo da Solução (Versão Inicial)
- Catálogo público (somente leitura para clientes).
- Área administrativa para cadastro/gerenciamento de peças.

## 4. Requisitos Funcionais (RF)
- **RF01**: Cadastrar peça (foto, descrição, tamanho, preço, categoria/condição).
- **RF02**: Listar peças no catálogo público.
- **RF03**: Filtrar/pesquisar por tamanho, categoria e texto.
- **RF04**: Editar e remover peça.
- **RF05**: Controlar disponibilidade (disponível/vendido).
- **RF06**: Autenticação para administrador (login).
- **RF07 (opcional)**: Relatório simples (itens mais visualizados/vendidos).
- **RF08 (opcional)**: “Favoritos” (cliente marca interesse sem login).

## 5. Requisitos Não Funcionais (RNF)
- **RNF01**: Interface responsiva (desktop e mobile).
- **RNF02**: Tempo de carregamento aceitável (páginas < 3s em rede comum).
- **RNF03**: Persistência em banco de dados.
- **RNF04**: Segurança básica de autenticação.
- **RNF05**: Código versionado e documentação em Markdown.
- **RNF06**: Padrão de commits descritivos (ex.: `feat: cadastro de peça`).

## 6. Personas (resumo)
- **Administrador(a)**: dono do brechó; precisa agilidade no cadastro e controle.
- **Cliente**: navega no catálogo, filtra por tamanho/categoria e avalia preço/condição.

## 7. Critérios de Aceitação (exemplos)
- Dado que estou no catálogo, quando pesquiso por “P/M”, então vejo apenas peças P ou M.
- Dado que estou logada como admin, quando salvo um cadastro completo, então a peça aparece no catálogo.

## 8. Riscos & Premissas
- **Riscos**: poucas fotos de qualidade; falta de padronização de medidas.
- **Premissas**: haverá ao menos 30 itens para testes; fotos em JPEG/PNG.


