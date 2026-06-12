# aula6
# Processamento de Sinais I — Aula Prática 6: Projeto de Filtros IIR

Este repositório contém os códigos e o relatório técnico da Aula Prática 6 (AP6), cujo tema principal é o Projeto, Análise e Implementação de Filtros Digitais com Resposta ao Impulso Infinita (IIR) utilizando Seções de Segunda Ordem (SOS). 

O trabalho aborda desde os conceitos geométricos elementares no Plano Z até a restauração de um sinal de áudio real corrompido, avaliando os impactos de diferentes topologias e da quantização de coeficientes em ponto fixo.

---

## Estrutura do Repositório

* codigos/ : Contém os scripts em Python com as rotinas de projeto de filtros, gráficos e processamento.
* audio/ : Contém o ficheiro original (handel.wav) e os ficheiros gerados pós-filtragem.
* graficos/ : Gráficos de magnitude, fase, planos de polos e zeros e análise FFT.
* Relatorio_PDS.docx : Relatório técnico completo com as devidas justificativas e equações matemáticas.
* README.md : Este documento com a descrição geral do projeto.

---

## Conteúdo do Projeto por Questão

### Questão 1: Blocos Componentes Básicos de 2ª Ordem
Implementação e análise detalhada de quatro estruturas básicas de segunda ordem operando em fs = 20000 Hz, variando o raio dos polos (r) em 0.8, 0.9 e 0.98:
* (a) Filtro Passa-Baixas (fc = 1000 Hz) com zeros em Nyquist.
* (b) Filtro Passa-Altas (fc = 2000 Hz) com zeros em DC.
* (c) Filtro Passa-Faixas (fc = 7000 Hz) com zeros em z = 1 e z = -1.
* (d) Filtro Notch (fc = 3000 Hz) com zeros sobre o círculo unitário.
O objetivo desta etapa foi demonstrar como o parâmetro r afeta diretamente a seletividade, a largura de banda e o tempo de acomodação do sistema.

### Questão 2: Filtro Passa-Faixas em Cascata (6000 Hz a 8000 Hz)
Desenvolvimento de uma estrutura composta de quarta ordem obtida pela associação em cascata (multiplicação) de um bloco passa-altas e um bloco passa-baixas de segunda ordem. Os resultados demonstram a obtenção de uma banda passante mais plana e uma transição de rejeição mais íngreme.

### Questão 3: Filtro Rejeita-Faixas em Paralelo (1000 Hz a 4000 Hz)
Implementação de um filtro rejeita-faixas por meio da associação em paralelo (soma) de estruturas passa-baixas e passa-altas. Esta questão traz uma discussão teórica importante sobre o efeito da fase não linear, evidenciando por que a soma desloca os zeros para fora do círculo unitário e limita a atenuação na banda de rejeição a apenas cerca de -5 dB.

### Questão 4: Sensibilidade e Impacto da Quantização de Coeficientes
Estudo comparativo dos efeitos de palavra digital de precisão finita em resoluções de 4, 8 e 16 bits. Os testes contrapõem o comportamento da Forma Direta Completa em relação à Forma em Blocos (SOS), ilustrando de forma prática o fenómeno da Instabilidade de Wilkinson, onde a forma em blocos prova ser muito mais robusta contra erros de arredondamento.

### Questão 5: Processamento de Sinal de Áudio Real (handel.wav)
Aplicação prática dos conceitos estudados na recuperação do ficheiro clássico de Handel corrompido por duas senoides analíticas e ruído branco. O projeto inclui:
* Mapeamento espectral das frequências de interferência em 100 Hz e 2000 Hz.
* Implementação de uma cascata de dois filtros Notch IIR de segunda ordem com r = 0.98.
* Levantamento estatístico de métricas quantitativas (SNR em dB e MSE) para as diferentes variâncias de ruído propostas (0.01, 0.1 e 1.0).
* Análise subjetiva de áudio focada na inteligibilidade do coro musical.
* Teste de quantização do filtro em 2, 4, 8 e 16 bits para avaliação de estabilidade.

---

## Tecnologias e Ferramentas
* Linguagem de Programação: Python 3
* Bibliotecas principais: numpy, scipy.signal, matplotlib

---

## Conclusões Gerais
O projeto permitiu validar que os filtros IIR alcançam excelente seletividade com ordens computacionais baixas. No entanto, demonstrou-se também a sensibilidade dessas estruturas a perturbações de fase e erros numéricos, consolidando a arquitetura em Seções de Segunda Ordem (SOS) em Cascata como a solução padrão para garantir estabilidade e fidelidade em sistemas de processamento comercial.
