<template>
  <div class="container">
    <div class="inputScreen">
      <div class="logoSection">
        <img class="logo" src="@/assets/logo.png" alt="" />
      </div>
      <div class="inputSection">
        <textarea
          class="textarea"
          v-model="inputData"
          placeholder="Ingrese el texto aquí"
          required
        ></textarea>
        <div class="send">
          <div class="btnMessage">
            <i class="fa-solid fa-circle-exclamation"></i>
            <p>Sólo letras minúsculas y sin acentos</p>
          </div>
          <div class="buttons">
            <button @click="clearData" class="clear">Limpiar</button>
            <div class="actionButtons">
              <button class="encrypt" @click="encryptData">Encriptar</button>
              <button class="decrypt" @click="decryptData">Desencriptar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="outputScreen">
      <div class="card">
        <h3 class="hide" :class="hide">El mensaje encriptado es:</h3>
        <p class="outputData">
          {{ encData }}
        </p>
        <div class="message" :class="show">
          <img class="doll" src="@/assets/doll.png" alt="" />
          <h3 class="cardMsg">Ningún mensaje fue encontrado</h3>
          <p class="desc">
            Ingresa el texto que deseas Encriptar o Desencriptar
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CryptoJS from "crypto-js";
export default {
  data() {
    return {
      inputData: "",
      secret: "123#$%",
      encData: "",
      show: "",
      hide: "",
    };
  },
  methods: {
    encryptData() {
      if (this.inputData.length) {
        const data = CryptoJS.AES.encrypt(
          this.inputData,
          this.secret
        ).toString();

        localStorage.setItem("secretData", data);

        this.getEncryptedData();
        this.show = "hide";
        this.hide = "show";
      }
    },

    decryptData() {
      const secretData = localStorage.getItem("secretData");
      const decryptData = CryptoJS.AES.decrypt(
        secretData,
        this.secret
      ).toString(CryptoJS.enc.Utf8);

      alert("Mensaje Desencriptado: " + decryptData);
    },

    clearData() {
      // remove data from localStorage
      this.inputData = "";
      this.show = "";
      this.encData = "";
      this.hide = "";
    },

    getEncryptedData() {
      this.encData = localStorage.getItem("secretData");
    },
  },
};
</script>

<style scoped>
.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
}
.inputScreen {
  width: 60vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.logoSection {
  padding: 0.5rem;
  display: flex;
  width: 100%;
}
.logo {
  height: 50px;
}
.inputSection {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.textarea {
  height: 300px;
  width: calc(100% - 30px);
  background-color: transparent;
  border: none;
  resize: none;
  outline: none;
  text-align: center;
  font-size: 32px;
  color: var(--darkBlue);
}
.send {
  width: calc(100% - 30px);
}
.btnMessage {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 16px;
  color: var(--grey);
  margin-bottom: 0.5rem;
}
.buttons {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.clear {
  border: solid 1px var(--red);
  background-color: var(--red);
  color: white;
  padding: 1rem 0;
  border-radius: 20px;
  font-size: 16px;
  cursor: pointer;
  transition: 0.4s;
  width: 100%;
}
.clear:hover {
  background-color: white;
  color: var(--red);
}
.actionButtons {
  padding-top: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
.encrypt {
  border: solid 1px var(--darkBlue);
  background-color: var(--darkBlue);
  color: white;
  padding: 1.3rem 0;
  border-radius: 24px;
  font-size: 16px;
  margin: 0 1rem 0 0;
  cursor: pointer;
  transition: 0.4s;
  width: 50%;
}
.encrypt:hover {
  background-color: white;
  color: var(--darkBlue);
}
.decrypt {
  border: solid 1px var(--grey);
  background-color: var(--mediumBlue);
  color: var(--grey);
  padding: 1.3rem 0;
  border-radius: 24px;
  font-size: 16px;
  cursor: pointer;
  transition: 0.4s;
  width: 50%;
}
.decrypt:hover {
  background-color: var(--grey);
  color: white;
}

.outputScreen {
  width: 40vw;
  height: 100vh;
}
.card {
  height: calc(100% - 80px);
  margin: 40px;
  background-color: white;
  box-shadow: 0px 24px 32px -8px rgba(0, 0, 0, 0.08);
  border-radius: 32px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.outputData {
  color: var(--darkBlue);
  text-align: center;
  max-width: calc(100% - 90px);
  word-break: break-all;
  overflow-y: auto;
}
.message {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.doll {
  width: calc(100% - 100px);
  height: calc(100% - 100px);
}
.cardMsg {
  margin-top: 2rem;
  width: 60%;
  text-align: center;
}
.desc {
  margin-top: 0.5rem;
  width: 60%;
  text-align: center;
}
.hide {
  display: none;
}
.show {
  display: flex;
}
/* RESPONSIVE SECTION */
@media screen and (max-width: 768px) {
  .container {
    display: flex;
    flex-direction: column;
    gap: 5rem;
  }
  .inputScreen {
    width: 100%;
    height: 40vh;
  }
  .textarea {
    font-size: 12px;
    height: 300px;
  }
  .card {
    width: calc(100% - 80px);
  }
  .outputScreen {
    width: 100vw;
  }
  .doll {
    display: none;
  }
  .cardMsg {
    margin-top: 0;
  }
  .desc {
    margin-top: 0;
  }
}
</style>
