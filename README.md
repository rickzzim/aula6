# aula6
# 🎵 Processamento de Sinais I — Aula Prática 6: Projeto de Filtros IIR

Este repositório contém a resolução computacional completa e o relatório técnico da **Aula Prática 6 (AP6)**, focada no **Projeto, Análise e Implementação de Filtros IIR (Resposta ao Impulso Infinita)** utilizando blocos estruturais de 2ª ordem (Seções de Segunda Ordem - SOS).

O projeto aborda desde a síntese geométrica elementar no Plano Z até a restauração de um sinal de áudio real corrompido, avaliando os impactos da topologia estrutural e da quantização de coeficientes em ponto fixo.

---

## 🚀 Estrutura do Repositório

* 📁 `codigos/` : Scripts em Python (`.py` ou `.ipynb`) contendo a implementação de todos os filtros, rotinas de quantização e processamento do áudio.
* 📁 `audio/` : Arquivo original (`handel.wav`), sinais contaminados matematicamente e arquivos resultantes pós-filtragem para fins de auditoria acústica.
* 📁 `graficos/` : Curvas de resposta em magnitude (dB), diagramas de polos e zeros e análise espectral via FFT gerados pelas simulações.
* 📄 `Relatorio_Aula_Pratica_6.docx` : Documento técnico completo formatado com as justificativas matemáticas e análises exigidas pelo roteiro.
* 📄 `README.md` : Este guia de navegação rápida para o professor.

---

## 📈 O que o Professor vai encontrar em cada Questão?

### Questão 1: Blocos Componentes Básicos de 2ª Ordem
A análise da influência geométrica do raio dos polos ($r \in \{0.8, 0.9, 0.98\}$) sobre quatro estruturas fundamentais amostradas a $f_s = 20\text{ kHz}$:
* **(a) Passa-Baixas ($f_c = 1000\text{ Hz}$):** Polos complexos com zeros em Nyquist ($z = -1$).
* **(b) Passa-Altas ($f_c = 2000\text{ Hz}$):** Polos complexos com zeros em DC ($z = 1$).
* **(c) Passa-Faixas ($f_c = 7000\text{ Hz}$):** Zeros distribuídos em $z = \pm 1$.
* **(d) Notch Filter ($f_c = 3000\text{ Hz}$):** Zeros de transmissão posicionados rigorosamente sobre o círculo unitário ($|z| = 1$).
* *Foco da Avaliação:* Demonstração analítica de como o aumento de $r$ eleva a **seletividade**, estreita a **largura de banda**, mas estende o tempo de acomodação da resposta ao impulso.

### Questão 2: Filtro Passa-Faixas em Cascata ($6000\text{ Hz}$ a $8000\text{ Hz}$)
* **Topologia:** Multiplicação de funções de transferência de 2ª ordem (Passa-Altas $\times$ Passa-Baixas) resultando em um sistema de 4ª ordem.
* *Foco da Avaliação:* Comparação de desempenho evidenciando a formação de uma banda passante plana com transições de rejeição significativamente mais íngremes do que as seções isoladas de 2ª ordem.

### Questão 3: Filtro Rejeita-Faixas em Paralelo ($1000\text{ Hz}$ a $4000\text{ Hz}$)
* **Topologia:** Soma algébrica de um bloco Passa-Baixas e um Passa-Altas.
* *Foco da Avaliação:* **Discussão teórica crucial sobre fase não linear.** O código demonstra que a soma puxa os zeros para *fora do círculo unitário*, gerando uma atenuação fraca na banda de rejeição (~ -5 dB). Prova por que a topologia paralela direta falha em criar "vales" profundos sem técnicas de equalização de fase.

### Questão 4: Sensibilidade da Quantização de Coeficientes
* **Metodologia:** Redução da palavra digital para $b \in \{4, 8, 16\}$ bits comparando a **Forma Direta Completa** (polinômio expandido) versus a **Forma em Blocos (SOS)**.
* *Foco da Avaliação:* Demonstração prática da Instabilidade de Wilkinson. Sob quantização severa de 4 bits, a Forma Direta sofre degradação catastrófica e deslocamento caótico de polos, enquanto a estrutura em blocos SOS preserva a integridade do contorno e a estabilidade assintótica.

### Questão 5: Restauração de Áudio Real (`handel.wav`)
Processamento real do sinal corrompido pela equação analítica:
$$y(t) = x(t) + 0.05\cos(200\pi t) + 0.075\sin(4000\pi t) + n(t)$$

* **Mapeamento de Interferências:** Identificação exata de tons espúrios em $100\text{ Hz}$ (zumbido grave) e $2000\text{ Hz}$ (apito agudo), além do ruído branco gaussiano.
* **Filtragem:** Projeto de uma cascata em série de dois filtros *Notch IIR de 2ª ordem* ($r = 0.98$) sintonizados nas frequências exatas.
* **Métricas Quantitativas Computadas:** Tabela comparativa de **SNR (dB)** e **MSE** para as variâncias $\sigma^2 \in \{0.01, 0.1, 1.0\}$.
* **Avaliação Subjetiva:** Discussão sobre o restabelecimento da inteligibilidade do coro clássico "Aleluia" e os limites lineares frente ao ruído branco interno à banda.
* **Análise de Hardware (Quantização):** Avaliação de estabilidade em $2, 4, 8$ e $16$ bits, comprovando o travamento de polos e zeros na estrutura SOS.

---

## 🛠️ Tecnologias Utilizadas
* **Linguagem:** Python 3.x
* **Bibliotecas Core:** `numpy`, `scipy.signal` (projeto de filtros, transformações Z e convoluções), `matplotlib.pyplot` (geração de gráficos), `scipy.io.wavfile` (I/O de áudio digital).

---

## 🎯 Conclusões Principais do Trabalho
1. Filtros IIR alcançam excelente seletividade com ordens muito inferiores às de filtros FIR equivalentes.
2. A associação paralela de blocos IIR básicos altera destrutivamente a posição dos zeros devido ao descasamento de fase natural de sistemas recursivos.
3. A implementação em **Seções de Segunda Ordem (SOS) em Cascata** é o padrão industrial obrigatório para mitigar o ruído de quantização e assegurar a estabilidade de filtros em processadores de ponto fixo comerciais.
