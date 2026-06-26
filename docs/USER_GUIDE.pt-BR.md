# Gerador de Etiquetas — Manual do Usuário e Documentação Técnica

Idiomas: [English](USER_GUIDE.md) · **Português (pt-BR)** · [简体中文](USER_GUIDE.zh-CN.md)

Autor: Jhon Lee Quint


## 1. PROPÓSITO DO SISTEMA
Esta ferramenta foi desenvolvida como um "Estúdio de Engenharia" (Software Standalone Offline) para a prototipagem rápida e impressão sob demanda de etiquetas industriais. O objetivo principal é permitir a criação de layouts, testes de códigos de barras (MAC, SN, EAN) e verificação direta em impressoras térmicas Zebra sem a necessidade de setups complexos ou conexão com a internet.

## 2. MANUAL DO USUÁRIO
- **Tamanho da Etiqueta:** Defina as dimensões reais (em milímetros) nos campos superiores (ex: 100 x 150) e clique em "Aplicar".
- **Adicionar Elementos:** Utilize os botões "+ Texto", "+ Forma", "+ Logo / Imagem" para compor o layout.
- **Códigos de Barras:** Selecione o padrão desejado no menu suspenso. Para padrões alfanuméricos (ex: MAC Address contendo letras), utilize EXCLUSIVAMENTE o padrão CODE-128. Padrões como EAN e UPC aceitam apenas números.
- **QR Code:** Clique em "+ QR Code" e insira a matriz de dados desejada.
- **Exportação (.Lab):** O botão "Salvar .Lab" exporta o projeto atual para uso futuro ou backup das coordenadas do layout.
- **Impressão (Rede):** O botão "Impressora Comum" gera uma rasterização da etiqueta e aciona o gerenciador de impressão nativo do sistema operacional (ideal para impressoras A4/Jato de Tinta conectadas em rede).
- **Impressão (Zebra/WebUSB):** Envia a conversão direta em linguagem ZPL (Zebra Programming Language) via cabo USB para impressoras térmicas da linha Zebra.

## 3. LIMITAÇÕES TÉCNICAS E ESCOPO
Por ser uma aplicação cliente (Client-Side) operando de forma offline no navegador, as seguintes limitações de engenharia aplicam-se ao escopo da ferramenta:
- **Ausência de Serialização em Lote:** O sistema não é projetado para integração com Banco de Dados ou ERP/MES para impressão sequencial automática (ex: imprimir 1.000 MAC Addresses sequenciais de forma autônoma). A operação é baseada no design unitário (WYSIWYG).
- **Armazenamento Volátil:** A ferramenta não possui recurso de "Auto-Salvar" em nuvem ou disco local. Se a aba do navegador for fechada ou atualizada acidentalmente sem que o projeto tenha sido exportado (.Lab), os dados em tela serão perdidos.
- **Conversão ZPL (Dithering):** Para impressão térmica WebUSB, imagens coloridas e gradientes passam por um algoritmo de Floyd-Steinberg (halftoning). Imagens com contrastes muito baixos podem sofrer degradação visual na impressão térmica de 1-bit.
- **Compatibilidade WebUSB:** A comunicação direta via porta USB exige navegadores baseados em Chromium (Google Chrome, Microsoft Edge). Navegadores baseados no motor Gecko (Mozilla Firefox) ou WebKit (Safari antigo) não suportam esta API de hardware.

## 4. ARQUITETURA E BIBLIOTECAS UTILIZADAS
O sistema foi construído sob uma arquitetura "Client-Side" pura (Single-Page Application / Arquivo Único), sem dependência de back-end (servidores), garantindo portabilidade e segurança em redes industriais isoladas (Air-Gapped).
- **Linguagens Base:** HTML5, CSS3 e Vanilla JavaScript (ECMAScript 6+).
- **Motor Gráfico (Canvas):** Fabric.js (v5.3.0) - Utilizado para a manipulação vetorial, arrastar e soltar (Drag and Drop) e renderização na escala física exata de 203 DPI.
- **Geração de Código de Barras:** JsBarcode (v3.11.5) - Responsável pela tradução matemática e rasterização (Padrões ISO) para CODE-128, EAN, UPC, etc.
- **Geração de Matriz de Dados:** qrcode.js (v1.5.1) - Processamento e geração vetorial do QR Code com correção de erro integrada.
- **API de Comunicação Física:** WebUSB API nativa do navegador - Permite o roteamento dos bytes seriais (algoritmo ZPL/GFA) do navegador diretamente para o EndPoint USB da impressora (Zebra Vendor ID 0x0A5F).
