# lecture_42_JS_Events_Ascent_and_dive  

При наступлении события – самый глубоко вложенный элемент, на котором оно произошло, помечается как «целевой» (**event.target**).  

-  Затем событие сначала двигается вниз от корня документа к event.target, по пути вызывая обработчики, поставленные через addEventListener(...., true), где true – это сокращение для {capture: true}.  
-  Далее обработчики вызываются на целевом элементе.  
-  Далее событие двигается от event.target вверх к корню документа, по пути вызывая обработчики, поставленные через on<event> и addEventListener без третьего аргумента или с третьим аргументом равным false.  
  
**Каждый обработчик имеет доступ к свойствам события event:**    
-  **event.target** – самый глубокий элемент, на котором произошло событие.  
-  **event.currentTarget** (=this) – элемент, на котором в данный момент сработал обработчик (тот, на котором «висит» конкретный обработчик)  
-  **event.eventPhase** – на какой фазе он сработал (погружение=1, фаза цели=2, всплытие=3).  
  
Любой обработчик может остановить событие вызовом **event.stopPropagation()**, но делать это не рекомендуется, так как в дальнейшем это событие может понадобиться, иногда для самых неожиданных вещей.  

В современной разработке стадия погружения используется очень редко, обычно события обрабатываются во время всплытия. И в этом есть логика.  

В реальном мире, когда происходит чрезвычайная ситуация, местные службы реагируют первыми. Они знают лучше всех местность, в которой это произошло, и другие детали.   Вышестоящие инстанции подключаются уже после этого и при необходимости.  

Тоже самое справедливо для обработчиков событий. Код, который «навесил» обработчик на конкретный элемент, знает максимум деталей об элементе и его предназначении. Например, обработчик на определённом `<td>` скорее всего подходит только для этого конкретного `<td>`, он знает все о нём, поэтому он должен отработать первым. Далее имеет смысл передать обработку события родителю – он тоже понимает, что происходит, но уже менее детально, далее – выше, и так далее, до самого объекта document, обработчик на котором реализовывает самую общую функциональность уровня документа.  

Всплытие и погружение являются основой для «делегирования событий» – очень мощного приёма обработки событий.   

