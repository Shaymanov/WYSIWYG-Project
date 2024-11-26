<template>
  <div class="iconsContainer">
    <div class="icons"> <img src="./components/icons/IconArrow.svg" ></div>
    <div class="icons"><img src="./components/icons/IconArrow.svg" class="reverseArrow"></div>
    <!-- <div @click="changeSelectionCase('uppercase')" class="icons"><img src="./components/icons/IconT.svg"></div> -->
    <div @click="transformSelectionToHeading" class="icons"><img src="./components/icons/IconT.svg"></div>
    <!-- <div @click="changeSelectionCase('lowercase')" class="icons"><img src="./components/icons/IconTwoT.svg"></div> -->
    <div @click="transformSelectionToParagraph" class="icons"><img src="./components/icons/IconTwoT.svg"></div>
    <div class="icons" @click="changeImage"> <img src="./components/icons/IconImage.svg" ></div>
    <div><button @click="copyFullHtml" class="copy">Скопировать HTML</button></div>
  </div>

  <div class="writeText">
    <p ref="textContent" contenteditable="true" @input="updateText" > 
    {{ text }}
  </p>
    
  <h1 ref="textContent" contenteditable="true"  @input="updateTexth1"> 
    {{ texth1 }}
  </h1>

  <img v-if="imageUrl" :src="imageUrl">
    
  <p ref="textContent" contenteditable="true" @input="updateText2">
    {{ text2 }}
  </p>
    
  <p ref="textContent" contenteditable="true" @input="updateText3" >
    {{ text3 }}
  </p>
</div>
  
</template>

<script lang="ts">
import { ref, computed } from 'vue';
import photo from './assets/Image/Image.png';



 export default {
  data() {

    const text = ref('Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.')

    const text2 = ref('Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.')

    const texth1 = ref('Смотрите какие обезьянки')

    const text3 = ref('Товарищи! новая модель организационной деятельности требуют от нас анализа направлений прогрессивного развития. Задача организации, в особенности же постоянный количественный рост и сфера нашей активности требуют от нас анализа позиций, занимаемых участниками в отношении поставленных задач. Задача организации, в особенности же реализация намеченных плановых заданий требуют от нас анализа системы обучения кадров, соответствует насущным потребностям.')

  
  // Преобразование текста в АБЗАЦ
  const textContent = ref(null);

  const transformSelectionToParagraph = () => {
  const selection = window.getSelection();
  const range = selection.getRangeAt(0);

  // Проверка выделения текста
  if (selection.toString().trim()) {
    let selectedText = selection.toString();

    // Заглавная буква
    selectedText = selectedText.charAt(0).toUpperCase() + selectedText.slice(1);

    const newParagraph = document.createElement('p');
    newParagraph.textContent = selectedText;

    range.deleteContents();
    range.insertNode(newParagraph);

    selection.removeAllRanges();
  } else {
        alert('Выделите текст');
      }
};



// Преобразование текста в ЗАГОЛОВОК
  const textContent2 = ref(null);

    const transformSelectionToHeading = () => {
      const selection = window.getSelection();
      const range = selection.getRangeAt(0);

      if (selection.toString().trim()) {
        let selectedText = selection.toString();

        selectedText = selectedText.charAt(0).toUpperCase() + selectedText.slice(1);

        const newHeading = document.createElement('h1');
        newHeading.textContent = selectedText;

        range.deleteContents();
        range.insertNode(newHeading);

        selection.removeAllRanges();
      } else {
        alert('Выделите текст');
      }
    };

    // не так понял задачу про абзацы
    // const changeSelectionCase = (caseType: string) => {
    //   const selection = window.getSelection();
    //   const range = selection.getRangeAt(0);

    //   if (selection.toString().trim()) {
    //     const selectedText = selection.toString();

    //     const transformedText =
    //       caseType === 'uppercase'
    //         ? selectedText.toUpperCase()
    //         : selectedText.toLowerCase();

    //     const span = document.createElement('span');
    //     span.textContent = transformedText;

    //     range.deleteContents();
    //     range.insertNode(span);

    //     selection.removeAllRanges();
    //   } else {
    //     alert('Выделите текст');
    //   }
    // };

    const imageUrl = ref(photo);

    const changeImage = () => {
      const url = prompt('Введите новый URL изображения:', imageUrl.value);
      if (url) {
        imageUrl.value = url;
      }
    };

    const copyFullHtml = () => {
        const fullHtml = document.documentElement.outerHTML;
        navigator.clipboard
          .writeText(fullHtml)    
    };

    const updateText = (event: Event) => {
      if (event.target instanceof HTMLElement){
      }
    };

    const updateTexth1 = (event: Event) => {
      if (event.target instanceof HTMLElement){
      }
    };

    const updateText2 = (event: Event) => {
      if (event.target instanceof HTMLElement){
      }
    };

    const updateText3 = (event: Event) => {
      if (event.target instanceof HTMLElement){
      }
    };

    return {

      transformSelectionToParagraph,
      textContent,

      transformSelectionToHeading,
      textContent2,

      // changeSelectionCase,

      copyFullHtml,
      
      text,
      updateText,
      
      texth1,
      updateTexth1,

      imageUrl,
      changeImage,
      
      text2,
      updateText2,
      
      text3,
      updateText3,
    }
  },
}
</script>

<style scoped>

.writeTextImage>img{
  max-width: 800px;
}

</style>