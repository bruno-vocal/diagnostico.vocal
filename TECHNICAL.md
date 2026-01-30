# 🔧 Documentação Técnica - VocalQuest

## Arquitetura do Sistema

### Visão Geral
VocalQuest é um SPA (Single Page Application) construído com HTML5, CSS3 e JavaScript vanilla (ES6+), utilizando a Web Audio API para funcionalidades de áudio avançadas.

---

## 📁 Estrutura de Arquivos

```
vocalquest/
│
├── index.html                    # Ponto de entrada, estrutura HTML
│
├── css/
│   └── style.css                # Estilos globais (~27KB)
│
├── js/
│   ├── data.js                  # Dados estáticos (lições, conquistas, loja)
│   ├── audio.js                 # Engine de áudio e análise de pitch
│   ├── exercises.js             # Renderização de exercícios
│   ├── gamification.js          # Sistema de gamificação e progresso
│   └── app.js                   # Lógica principal da aplicação
│
├── README.md                     # Documentação principal
└── GUIA-RAPIDO.md               # Guia do usuário
```

---

## 🗄️ Esquema de Dados

### Tabelas do Banco de Dados

#### **users**
```javascript
{
  id: string,                    // UUID gerado automaticamente
  username: string,              // Nome de exibição do usuário
  email: string,                 // Email único para login
  level: number,                 // Nível do usuário (calculado por XP)
  xp: number,                    // Pontos de experiência totais
  coins: number,                 // Moedas virtuais
  streak: number,                // Dias consecutivos de prática
  lastPracticeDate: string,      // Data da última prática (ISO 8601)
  avatarBody: string,            // Cor do corpo (hex)
  avatarHair: string,            // Estilo de cabelo
  avatarAccessory: string,       // Acessório equipado
  totalLessonsCompleted: number  // Total de lições completas
}
```

#### **progress**
```javascript
{
  id: string,                    // UUID
  userId: string,                // Referência ao usuário
  lessonId: string,              // ID da lição (ex: "b1", "i3")
  completed: boolean,            // Se foi completada
  stars: number,                 // Estrelas obtidas (0-3)
  score: number,                 // Pontuação percentual (0-100)
  attempts: number,              // Número de tentativas
  completedDate: string          // Data de conclusão (ISO 8601)
}
```

#### **achievements**
```javascript
{
  id: string,                    // UUID
  userId: string,                // Referência ao usuário
  achievementId: string,         // ID da conquista (ex: "first_lesson")
  unlockedDate: string,          // Data de desbloqueio (ISO 8601)
  title: string,                 // Título da conquista
  description: string            // Descrição da conquista
}
```

#### **leaderboard**
```javascript
{
  id: string,                    // UUID
  userId: string,                // Referência ao usuário
  username: string,              // Nome de exibição
  weeklyXp: number,              // XP acumulado na semana
  totalXp: number,               // XP total do usuário
  week: string                   // Identificador da semana (ex: "2026-W05")
}
```

---

## 🎨 Classes JavaScript Principais

### **AudioEngine** (audio.js)
Gerencia toda a funcionalidade de áudio da aplicação.

#### Métodos Principais:
```javascript
initialize()                     // Inicializa AudioContext e microfone
startRecording()                 // Inicia gravação de áudio
stopRecording()                  // Para gravação e retorna blob
getCurrentPitch()                // Obtém frequência atual em Hz
frequencyToNote(freq)            // Converte Hz para nota musical
noteToFrequency(note)            // Converte nota para Hz
isPitchCorrect(current, target)  // Verifica se afinação está correta
playTone(frequency, duration)    // Toca tom de referência
visualizePitch(canvas)           // Visualização em tempo real
autoCorrelate(buffer, sampleRate) // Algoritmo de detecção de pitch
```

#### Propriedades:
```javascript
audioContext      // Web Audio API context
analyser          // AnalyserNode para análise de frequência
microphone        // MediaStreamSource do microfone
isRecording       // Estado de gravação
mediaRecorder     // MediaRecorder API
```

---

### **Metronome** (audio.js)
Metrônomo digital com BPM ajustável.

#### Métodos:
```javascript
initialize()           // Cria AudioContext
start(tempo)           // Inicia metrônomo (BPM)
stop()                 // Para metrônomo
playClick()            // Toca um clique
setTempo(tempo)        // Ajusta BPM
```

---

### **ExerciseRenderer** (exercises.js)
Renderiza e gerencia diferentes tipos de exercícios.

#### Métodos:
```javascript
renderExercise(exercise, container)  // Renderiza exercício no DOM
renderQuiz(exercise, container)      // Renderiza quiz múltipla escolha
renderTrueFalse(exercise, container) // Renderiza verdadeiro/falso
renderMultipleChoice(exercise, container) // Múltipla seleção
renderRecord(exercise, container)    // Exercício de gravação
renderPitch(exercise, container)     // Exercício de afinação
checkAnswer()                        // Verifica resposta do usuário
showFeedback(isCorrect)              // Mostra feedback visual
cleanup()                            // Limpa recursos
```

#### Tipos de Exercícios:
1. **quiz**: Múltipla escolha (1 resposta correta)
2. **trueFalse**: Verdadeiro ou Falso
3. **multipleChoice**: Múltipla seleção (várias corretas)
4. **record**: Gravação de voz com duração mínima
5. **pitch**: Correspondência de afinação com nota-alvo

---

### **GamificationSystem** (gamification.js)
Sistema completo de gamificação e progressão.

#### Métodos Principais:
```javascript
calculateXPForLevel(level)           // Calcula XP necessário para nível
getLevelFromXP(xp)                   // Obtém nível atual do XP
getXPProgress(xp)                    // Progresso do nível atual
addRewards(xp, coins)                // Adiciona XP e moedas
updateStreak()                       // Atualiza streak diário
recordLessonProgress(lessonId, stars, score) // Registra progresso
checkAchievements()                  // Verifica e desbloqueia conquistas
unlockAchievement(achievement)       // Desbloqueia conquista
updateLeaderboard()                  // Atualiza ranking semanal
getNextLesson()                      // Retorna próxima lição
calculateStars(correct, total)       // Calcula estrelas (0-3)
```

#### Propriedades:
```javascript
currentUser          // Objeto do usuário atual
userProgress         // Array de progresso de lições
userAchievements     // Array de conquistas desbloqueadas
```

---

## 🔄 Fluxo de Dados

### Login/Registro
```
User Input → Fetch API → Table Users → LocalStorage → App State
```

### Completar Lição
```
Exercise Completion → Calculate Results → Update Progress → 
Add Rewards → Check Achievements → Update UI → Update Leaderboard
```

### Gravação de Áudio
```
User Clicks Record → getUserMedia() → MediaRecorder → 
AudioAnalyser → Pitch Detection → Visual Feedback → 
Stop Recording → Save Blob
```

---

## 🎵 Algoritmo de Detecção de Pitch

### Autocorrelação
O sistema usa **autocorrelação** para detectar a frequência fundamental da voz:

```javascript
autoCorrelate(buffer, sampleRate) {
  // 1. Calcula RMS para filtrar silêncio
  // 2. Encontra melhor offset de correlação
  // 3. Retorna frequência = sampleRate / offset
}
```

#### Vantagens:
- ✅ Funciona em tempo real
- ✅ Robusto a ruído
- ✅ Não requer bibliotecas externas
- ✅ Leve e eficiente

#### Limitações:
- ⚠️ Sensível a volume muito baixo
- ⚠️ Pode ter dificuldades com múltiplas vozes
- ⚠️ Requer ambiente relativamente silencioso

---

## 🎯 Sistema de Progressão

### Cálculo de Nível
```javascript
// XP necessário por nível
Level 1: 0-100 XP
Level 2: 100-250 XP
Level 3: 250-450 XP
Level N: sum(level * 100 + (level-1) * 50)
```

### Cálculo de Estrelas
```javascript
100% de acertos = 3 estrelas ⭐⭐⭐
80-99% = 2 estrelas ⭐⭐
60-79% = 1 estrela ⭐
< 60% = 0 estrelas (tentar novamente)
```

### Recompensas por Lição
| Nível | XP | Moedas |
|-------|----|----|
| Iniciante | 50-70 | 20-30 |
| Intermediário | 80-100 | 35-45 |
| Avançado | 120-140 | 50-60 |
| Profissional | 150-170 | 70-80 |

---

## 🔐 Segurança e Privacidade

### Dados do Usuário
- Senhas **NÃO são armazenadas** (sistema simplificado)
- Email usado apenas para identificação
- Dados persistidos em tabelas do servidor
- LocalStorage usado apenas para sessão

### Áudio
- Gravações **não são salvas** no servidor
- Processamento acontece localmente
- Blobs de áudio descartados após análise
- Microfone desativado após uso

---

## 🚀 Performance

### Otimizações Implementadas

#### JavaScript
- Event delegation para listas grandes
- Debounce em pitch detection
- Lazy loading de exercícios
- Cleanup de recursos de áudio

#### CSS
- Animações com `transform` (GPU)
- `will-change` para elementos animados
- Transições CSS em vez de JS quando possível

#### Áudio
- FFT size otimizado (2048)
- Análise limitada a necessário
- Cleanup de contextos de áudio

---

## 🧪 Testing

### Testes Manuais Recomendados

#### Funcionalidade Básica
- [ ] Login e registro funcionam
- [ ] Dashboard carrega corretamente
- [ ] Navegação entre páginas
- [ ] Perfil exibe dados corretos

#### Lições
- [ ] Abrir lição inicia corretamente
- [ ] Todos tipos de exercícios renderizam
- [ ] Progresso atualiza na barra
- [ ] Vidas diminuem em erros
- [ ] Resultados aparecem ao final

#### Áudio
- [ ] Microfone é solicitado
- [ ] Gravação inicia/para
- [ ] Pitch detection funciona
- [ ] Visualização aparece
- [ ] Tons de referência tocam

#### Gamificação
- [ ] XP e moedas são adicionados
- [ ] Streak atualiza corretamente
- [ ] Conquistas desbloqueiam
- [ ] Leaderboard funciona

#### Responsividade
- [ ] Desktop (1920x1080)
- [ ] Tablet (768x1024)
- [ ] Mobile (375x667)

---

## 🐛 Troubleshooting

### Problema: Microfone não funciona
**Solução:**
1. Verificar permissões do navegador
2. Usar HTTPS ou localhost
3. Testar em Chrome/Edge (melhor suporte)

### Problema: Pitch não detecta
**Solução:**
1. Aumentar volume do microfone
2. Cantar mais alto
3. Reduzir ruído ambiente
4. Verificar se microfone está ativo

### Problema: Dados não salvam
**Solução:**
1. Verificar conexão com API
2. Limpar LocalStorage e relogar
3. Verificar console para erros

### Problema: Animações travadas
**Solução:**
1. Reduzir complexidade visual
2. Desabilitar extensões do navegador
3. Atualizar navegador
4. Verificar GPU acceleration

---

## 📊 Métricas e Analytics

### Eventos Importantes para Tracking
```javascript
// Usuário
- user_register
- user_login
- user_logout

// Lições
- lesson_start
- lesson_complete
- lesson_fail
- exercise_complete
- exercise_error

// Gamificação
- achievement_unlock
- level_up
- streak_milestone

// Áudio
- microphone_permission
- recording_start
- recording_complete
- pitch_success
```

---

## 🔧 Configuração de Desenvolvimento

### Requisitos
- Servidor web (para APIs de tabelas)
- Navegador moderno (Chrome 90+, Firefox 88+, Edge 90+)
- HTTPS ou localhost (para getUserMedia)

### Variáveis de Ambiente
Não há variáveis de ambiente. Tudo é client-side.

### Build
Não requer build. É vanilla JavaScript.

---

## 📝 Convenções de Código

### JavaScript
- Usar camelCase para variáveis e funções
- Usar PascalCase para classes
- Comentários em português
- JSDoc para funções públicas principais

### CSS
- BEM-like naming quando apropriado
- Variáveis CSS para cores e espaçamentos
- Mobile-first approach
- Evitar !important

### HTML
- Semântico e acessível
- IDs para elementos únicos
- Classes para estilos
- Data attributes para configuração

---

## 🚀 Deploy

### Checklist para Produção
- [ ] Minificar CSS e JavaScript
- [ ] Otimizar imagens (se adicionar)
- [ ] Configurar HTTPS
- [ ] Testar em múltiplos navegadores
- [ ] Verificar responsividade
- [ ] Testar microfone em produção
- [ ] Configurar CORS se necessário
- [ ] Adicionar analytics (opcional)

### Ambientes Suportados
- ✅ Chrome/Edge 90+
- ✅ Firefox 88+
- ✅ Safari 14+ (limitado)
- ✅ Mobile Chrome/Safari
- ❌ Internet Explorer

---

## 📚 Referências Técnicas

### Web APIs Utilizadas
- [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- [MediaRecorder API](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder)
- [getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)
- [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [LocalStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

### Algoritmos
- Autocorrelação: [DSP Guide](http://www.dspguide.com/)
- Pitch Detection: [YIN Algorithm](http://audition.ens.fr/adc/pdf/2002_JASA_YIN.pdf)

---

## 🤝 Contribuindo

### Como Adicionar Novas Lições
1. Edite `js/data.js`
2. Adicione nova lição em `LESSONS_DATA[level].lessons`
3. Defina exercícios com tipos suportados
4. Teste todos os exercícios

### Como Adicionar Novas Conquistas
1. Edite `js/data.js`
2. Adicione em array `ACHIEVEMENTS`
3. Implemente lógica em `GamificationSystem.checkAchievements()`

### Como Adicionar Itens na Loja
1. Edite `js/data.js`
2. Adicione em `SHOP_ITEMS[category]`
3. Implemente funcionalidade em `app.js` se necessário

---

## 📄 Licença

Este projeto é educacional e de código aberto.  
Consulte LICENSE para mais informações.

---

**Documentação atualizada em:** 30 de Janeiro de 2026  
**Versão:** 1.0.0  
**Autor:** VocalQuest Development Team
