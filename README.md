# 🎤 VocalQuest - Aplicativo Gamificado de Técnica Vocal

![VocalQuest](https://img.shields.io/badge/VocalQuest-v1.0-green) ![Status](https://img.shields.io/badge/Status-Completo-success)

**VocalQuest** é um aplicativo web completo e totalmente interativo para aprendizado de técnica vocal, inspirado no Duolingo. O app oferece uma experiência gamificada, progressiva e divertida para cantores de todos os níveis aprenderem e praticarem técnica vocal profissional.

---

## 🎯 Funcionalidades Principais Implementadas

### ✅ Sistema de Autenticação
- Login e registro de usuários
- Armazenamento de progresso individual
- Perfil personalizável com avatar

### ✅ Sistema de Lições Progressivo
**4 Níveis de Dificuldade:**

#### 🌱 **Nível Iniciante**
1. Introdução à Respiração Diafragmática
2. Postura Vocal Correta
3. Aquecimento Básico
4. Vibração Labial e Lingual
5. Ressonância e Colocação

#### 🔵 **Nível Intermediário**
1. Articulação e Dicção
2. Extensão Vocal - Graves (Registro de Peito)
3. Extensão Vocal - Agudos (Registro de Cabeça)
4. Controle de Afinação
5. Sustentação de Notas

#### 🟣 **Nível Avançado**
1. Registro Misto (Mix Voice)
2. Belting Seguro
3. Vibrato Controlado
4. Runs e Melismas
5. Interpretação Avançada

#### 💜 **Nível Profissional**
1. Whistle Register
2. Distorção Vocal Segura
3. Harmonização Vocal
4. Improvisação Vocal
5. Performance e Palco

**Total: 20 lições completas com 80+ exercícios interativos**

### ✅ Tipos de Exercícios Interativos

1. **Quiz de Múltipla Escolha** - Teste seus conhecimentos teóricos
2. **Verdadeiro ou Falso** - Valide conceitos de técnica vocal
3. **Múltipla Seleção** - Identifique conceitos relacionados
4. **Gravação de Áudio** - Grave sua voz e pratique exercícios
5. **Análise de Pitch** - Combine sua afinação com notas-alvo
6. **Visualização em Tempo Real** - Veja sua voz em gráficos

### ✅ Sistema de Gamificação Completo

#### 🏆 Pontos e Recompensas
- **XP (Experiência)**: Ganhe XP completando lições
- **Moedas Virtuais**: Use para comprar itens na loja
- **Sistema de Níveis**: Progrida através de níveis de usuário
- **Estrelas**: Ganhe 1-3 estrelas por lição baseado no desempenho

#### 🔥 Sistema de Streak
- Contador de dias consecutivos
- Motivação para prática diária
- Meta diária de 3 exercícios

#### ❤️ Sistema de Vidas
- 5 vidas por lição
- Perca vidas ao errar exercícios
- Incentiva atenção e foco

#### 🎖️ Conquistas (Achievements)
- **Primeiros Passos**: Complete sua primeira lição
- **Sequência de 7 Dias**: Pratique por 7 dias consecutivos
- **Perfeição Total**: Complete uma lição sem erros
- **Iniciante Completo**: Complete todos os níveis iniciantes
- **Centurião Vocal**: Complete 100 exercícios
- **Mestre Vocal**: Complete todos os níveis
- **Cantor Milionário**: Acumule 1000 moedas
- **Mestre da Experiência**: Alcance 5000 XP

### ✅ Funcionalidades de Áudio Avançadas

#### 🎵 Web Audio API
- **Gravação de Voz**: Grave exercícios vocais diretamente no navegador
- **Detecção de Pitch**: Análise em tempo real de frequência vocal
- **Visualização de Frequência**: Gráficos visuais de sua voz
- **Player de Tons de Referência**: Ouça notas-alvo para praticar afinação
- **Metrônomo Integrado**: Pratique com controle de tempo (BPM ajustável)

#### 🎼 Análise Vocal
- Autocorrelação para detecção precisa de pitch
- Conversão de frequência para nota musical
- Verificação de afinação com tolerância configurável
- Medição de volume em tempo real

### ✅ Interface e Design

#### 🎨 Design Moderno
- Interface colorida inspirada no Duolingo
- Cores primárias: Verde (#58cc02), Azul (#1cb0f6), Roxo (#ce82ff), Rosa (#ff4b8e)
- Animações suaves e feedback visual imediato
- Design responsivo (mobile-first)
- Mascote animado (🎤)

#### 📱 Navegação Intuitiva
- **Home/Dashboard**: Progresso geral, streak, próxima lição, metas diárias
- **Mapa de Lições**: Estrutura em árvore progressiva
- **Prática Livre**: Acesso a lições desbloqueadas
- **Ranking**: Leaderboard semanal competitivo
- **Loja**: Compre itens com moedas virtuais
- **Perfil**: Estatísticas, conquistas, configurações

### ✅ Sistema de Loja Virtual
- **Customização de Avatar**: Cores, cabelos, acessórios
- **Boosts**: XP duplo, moedas duplas
- **Consumíveis**: Restaurar vidas, pular exercícios
- **Temas Visuais**: Escuro, Oceano, Pôr do Sol, Neon

### ✅ Sistema de Ranking
- Leaderboard semanal
- Competição entre usuários
- Pódio visual para top 3
- Atualização automática de pontuação

---

## 🗂️ Estrutura do Projeto

```
vocalquest/
├── index.html              # Página principal
├── css/
│   └── style.css          # Estilos completos (27KB+)
└── js/
    ├── data.js            # Dados das lições e conquistas (51KB+)
    ├── audio.js           # Engine de áudio e análise (10KB+)
    ├── exercises.js       # Sistema de exercícios interativos (19KB+)
    ├── gamification.js    # Sistema de gamificação (15KB+)
    └── app.js             # Aplicação principal (27KB+)
```

---

## 📊 Modelos de Dados

### Users (Usuários)
```javascript
{
  id: string,
  username: string,
  email: string,
  level: number,
  xp: number,
  coins: number,
  streak: number,
  lastPracticeDate: string,
  avatarBody: string,
  avatarHair: string,
  avatarAccessory: string,
  totalLessonsCompleted: number
}
```

### Progress (Progresso)
```javascript
{
  id: string,
  userId: string,
  lessonId: string,
  completed: boolean,
  stars: number (0-3),
  score: number,
  attempts: number,
  completedDate: string
}
```

### Achievements (Conquistas)
```javascript
{
  id: string,
  userId: string,
  achievementId: string,
  unlockedDate: string,
  title: string,
  description: string
}
```

### Leaderboard (Ranking)
```javascript
{
  id: string,
  userId: string,
  username: string,
  weeklyXp: number,
  totalXp: number,
  week: string
}
```

---

## 🚀 Como Usar

### Primeira Vez
1. **Abra o aplicativo** no navegador
2. **Crie uma conta** com nome de usuário e email
3. **Comece sua jornada** pelo nível Iniciante

### Navegação
1. **Dashboard**: Veja seu progresso e continue de onde parou
2. **Mapa de Lições**: Escolha lições desbloqueadas
3. **Complete Exercícios**: Responda quizzes, grave sua voz, pratique afinação
4. **Ganhe Recompensas**: XP, moedas e conquistas
5. **Compre na Loja**: Personalize seu avatar e compre boosts
6. **Compete no Ranking**: Veja sua posição semanal

### Dicas
- 🎯 **Mantenha seu streak**: Pratique todos os dias
- ⭐ **Busque 3 estrelas**: Complete lições perfeitamente
- 🎤 **Use fones de ouvido**: Para melhor qualidade nos exercícios de áudio
- 🔊 **Permita acesso ao microfone**: Necessário para exercícios de gravação

---

## 🎮 Mecânicas de Jogo

### Sistema de Progressão
- Lições desbloqueiam sequencialmente
- Lições anteriores devem ser completadas
- 4 níveis de dificuldade progressiva

### Sistema de Pontuação
- **3 Estrelas**: 100% de acertos
- **2 Estrelas**: 80%+ de acertos
- **1 Estrela**: 60%+ de acertos
- **0 Estrelas**: Menos de 60% (tente novamente)

### Recompensas por Lição
- **Iniciante**: 50-70 XP, 20-30 moedas
- **Intermediário**: 80-100 XP, 35-45 moedas
- **Avançado**: 120-140 XP, 50-60 moedas
- **Profissional**: 150-170 XP, 70-80 moedas

---

## 🎵 Conteúdo Pedagógico

O aplicativo cobre todo o espectro de técnica vocal profissional:

### Fundamentos
✅ Respiração diafragmática  
✅ Postura e alinhamento corporal  
✅ Aquecimento vocal  
✅ Ressonância e colocação  

### Técnicas Intermediárias
✅ Articulação e dicção  
✅ Extensão vocal (graves e agudos)  
✅ Controle de afinação  
✅ Sustentação de notas  

### Técnicas Avançadas
✅ Registro misto  
✅ Belting seguro  
✅ Vibrato natural  
✅ Runs e melismas  
✅ Interpretação expressiva  

### Técnicas Profissionais
✅ Whistle register  
✅ Distorção vocal controlada  
✅ Harmonização  
✅ Improvisação (scat singing)  
✅ Presença de palco  

---

## 🔧 Tecnologias Utilizadas

### Frontend
- **HTML5**: Estrutura semântica
- **CSS3**: Animações e design moderno
- **JavaScript (ES6+)**: Lógica da aplicação

### APIs e Recursos
- **Web Audio API**: Gravação e análise de áudio
- **MediaRecorder API**: Captura de voz
- **Fetch API**: Comunicação com banco de dados
- **LocalStorage**: Persistência de sessão

### Backend (RESTful API)
- **Tables API**: CRUD completo para dados
- Endpoints: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`
- Paginação e busca integradas

### Bibliotecas
- **Font Awesome 6**: Ícones
- **Google Fonts (Nunito)**: Tipografia

---

## ✨ Diferenciais

### 🎯 Totalmente Funcional
- Todas as funcionalidades implementadas e testadas
- Sistema completo de dados persistentes
- Interatividade total

### 🎵 Áudio Real
- Gravação de voz funcionando
- Análise de pitch em tempo real
- Feedback visual imediato

### 🏆 Gamificação Completa
- Sistema de recompensas balanceado
- Motivação através de conquistas
- Competição saudável no ranking

### 📚 Conteúdo Rico
- 20 lições completas
- 80+ exercícios variados
- Progressão pedagógica cuidadosa

### 🎨 Design Profissional
- Interface moderna e atrativa
- Animações suaves
- Responsivo e acessível

---

## 📈 Próximos Passos Recomendados

### Melhorias Futuras
1. **Análise de Voz Avançada**
   - Detecção de vibrato
   - Análise de timbre
   - Comparação com referências profissionais

2. **Conteúdo Adicional**
   - Mais lições por nível
   - Exercícios de músicas populares
   - Desafios temáticos semanais

3. **Social**
   - Sistema de amigos
   - Compartilhar conquistas
   - Grupos de estudo

4. **Monetização**
   - Plano premium com lições exclusivas
   - Aulas ao vivo com professores
   - Certificados de conclusão

5. **Mobile App**
   - Aplicativo nativo iOS/Android
   - Notificações push
   - Prática offline

6. **IA e Machine Learning**
   - Feedback personalizado por IA
   - Recomendações de exercícios
   - Avaliação automática de qualidade vocal

---

## 🎓 Público-Alvo

- 🎤 **Iniciantes** que querem aprender técnica vocal
- 🎸 **Cantores amadores** buscando melhorar
- 🎭 **Estudantes de canto** para prática complementar
- 🎼 **Profissionais** que querem manter prática diária
- 👨‍🏫 **Professores de canto** como ferramenta auxiliar

---

## 💡 Conceitos Aplicados

### Gamificação
- Pontos e níveis
- Recompensas e incentivos
- Progressão clara
- Feedback imediato
- Competição e ranking

### UX/UI Design
- Design centrado no usuário
- Feedback visual constante
- Navegação intuitiva
- Microinterações
- Acessibilidade

### Pedagogia Musical
- Progressão do simples ao complexo
- Variedade de exercícios
- Repetição espaçada
- Prática deliberada
- Avaliação formativa

---

## 📝 Licença e Créditos

**VocalQuest** - Aplicativo educacional de técnica vocal gamificado  
Desenvolvido como projeto educacional completo  
2024 - Todos os direitos reservados

### Inspirações
- Duolingo (gamificação e UX)
- Yousician (educação musical)
- Sing Sharp (análise de pitch)

---

## 🎉 Status do Projeto

✅ **COMPLETO E FUNCIONAL**

Todas as funcionalidades principais foram implementadas:
- ✅ Sistema de autenticação
- ✅ 20 lições completas (4 níveis)
- ✅ 80+ exercícios interativos
- ✅ Sistema de gravação e análise de áudio
- ✅ Gamificação completa (XP, moedas, streak, vidas)
- ✅ 8 conquistas implementadas
- ✅ Ranking semanal
- ✅ Loja virtual com 15+ itens
- ✅ Perfil de usuário completo
- ✅ Dashboard interativo
- ✅ Design responsivo e moderno

**O aplicativo está pronto para uso e deployment!** 🚀

---

## 📞 Suporte

Para dúvidas, sugestões ou reportar bugs, entre em contato através dos canais de suporte do projeto.

**Comece sua jornada vocal hoje com VocalQuest!** 🎤✨
