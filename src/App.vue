<script>
export default {
  data() {
    return {
      isAvalaible: true,
      isAvalaibleSecond: false,
    };
  },
  methods: {
    StartDownload(event) {
      // TORNANDO DISBABLE OS BOTÕES
      this.isAvalaible = false;
      this.isAvalaibleSecond = true
      const startButton = document.getElementById("startButton");
      startButton.classList.add("isDisabled");
      const cancelButton = document.getElementById("cancel");
      cancelButton.classList.remove("isDisabled");
      const progressDinamic = document.getElementById("progressDinamic");
      const porcent = document.getElementById("porcent");
      progressDinamic.classList.remove("bg-red-300");
      progressDinamic.classList.add("bg-green-500");

      let progressRem = 0;
      let porcentValue = 0;
      const interval = setInterval(() => {
        // ADICIONA SEMPRE +1 A CADA  0.8 SEGUNDOS
        progressRem += 1;
        porcentValue = progressRem;
        progressDinamic.style.width = progressRem + "%";
        porcent.textContent = `${porcentValue}%`;
        if (progressRem >= 100) {
          clearInterval(interval);
          isAvalaibleSecond: false
          startButton.classList.remove("isDisabled");
        }
      }, 800);

      // PARANDO O DOWNLOAD
      cancelButton.addEventListener("click", () => {
        clearInterval(interval);
        progressDinamic.classList.add("bg-red-300");
        event.target.textContent = "Retornar";
        this.isAvalaibleSecond = false
        startButton.classList.remove("isDisabled");
      });
    },
  },
};
</script>

<template>
  <div
    id="container"
    class="w-full h-screen flex space-y-6 flex-col items-center justify-center"
  >
    <div
      id=""
      class="cardProgress bg-zinc-800 rounded-md p-5 ring-1 ring-zinc-700"
    >
      <header class="flex w-full items-center justify-between">
        <h4 class="font-semibold text-zinc-100">Status de Transferência</h4>
        <div>
          <button class="text-red-400 transition-all hover:text-red-600">
            <i class="bi bi-x-lg"></i>
          </button>
        </div>
      </header>
      <main>
        <div class="flex items-center space-x-3 mt-5">
          <div>
            <i class="bi bi-archive-fill text-4xl text-green-500"></i>
          </div>
          <div class="flex flex-col gap-1">
            <small class="text-zinc-200">TemplateComponent-1.0.0.zip</small>
            <small classe="text-zinc-200">Tamanho: <span class="font-semibold text-zinc-200">36MB</span></small>
          </div>
        </div>
        <!-- Progresso -->
        <div class="mt-3 flex items-center gap-1 flex-nowrap">
          <small classe="text-zinc-200">Progresso:</small>
          <small id="porcent" class="text-green-300 font-semibold">0%</small>
        </div>
        <div
          class="block overflow-hidden w-full bg-zinc-600 h-2 rounded-full mt-4"
          id="progress"
        >
          <div
            class="block transition-all bg-green-500 rounded-full h-2"
            id="progressDinamic"
          ></div>
        </div>

        <div class="mt-4 flex w-full justify-end space-x-2">
          <button
            @click="StartDownload"
            id="startButton"
            :disabled="isAvalaibleSecond"
            class="px-5 rounded-md py-2 bg-green-600 transition-all hover:bg-green-500 text-white font-semibold"
          >
            Iniciar
          </button>
          <button
            :disabled="isAvalaible"
            id="cancel"
            class="px-5 isDisabled rounded-md py-2 bg-zinc-900 transition-all hover:bg-red-500 text-white font-semibold"
          >
            Cancelar
          </button>
        </div>
      </main>
    </div>
    <div>
      <footer class="max-w-5xl w-full flex items-center space-x-2">
        <div>
          <small>
            <a
              href="https://github.com/mariosalembe23"
              class="text-zinc-300 transition-all hover:underline hover:text-white"
              >Mário Lino Salembe</a
            >
          </small>
        </div>
        <div>|</div>
        <div>
          <small class="text-green-500 font-semibold">CodeJourney</small>
        </div>
      </footer>
    </div>
  </div>
</template>

<style scoped>
.cardProgress {
  max-width: 37rem;
  width: 90%;
}
#progressDinamic {
  width: 0;
}
button {
  font-size: 14px;
}
.isDisabled {
  opacity: 0.3;
}
.white-text{
  color: #fff !important;
}
</style>
