<template>
  <v-layout row>
    <v-flex lg3 class="p-0" style="border-right: 1px solid #c1c1c1 !important">
      <div class="d-flex align-items-center justify-content-between p-2">
        <b-button
          class="buttonNavchat novoCtt"
          pill
          variant="transparent"
          size="lg"
          style=""
        >
          <b-icon icon="plus-lg"></b-icon>
          <span> Novo Contato</span>
        </b-button>
        <div class="d-flex gap-2 p-2">
          <b-avatar variant="info" :src="avatarImg" size="4rem"></b-avatar>
          <div>
            <h5 class="m-0">Atendente 1</h5>
            <p>
              Online
              <b-icon
                icon="circle-fill"
                variant="success"
                font-scale="0.5"
              ></b-icon>
            </p>
          </div>
        </div>
        <b-icon
          icon="three-dots-vertical"
          scale="2rem"
          v-b-toggle.sidebarUserInfo
        ></b-icon>
      </div>
      <div class="p-3">
        <b-input-group class="mt-1">
          <b-form-input></b-form-input>
          <b-input-group-append>
            <b-button
              style="
                border-radius: 0px 5px 5px 0 !important;
                background: #054d86;
                color: #fff;
              "
              ><b-icon
                icon="search"
                variant="light
            "
              ></b-icon
            ></b-button>
          </b-input-group-append>
        </b-input-group>
      </div>

      <b-tabs
        content-class="mt-3"
        active-nav-item-class="bg-primary text-light"
        class="mt-3"
        fill
      >
        <b-tab active>
          <template #title>
            <b-icon icon="check-circle"></b-icon> Ativos
          </template>
          <div
            class="d-flex gap-2 p-2"
            v-for="conversa in conversas"
            :key="conversa.id"
            style="
              border-bottom: 1px solid #e7e7e7;
              padding-left: 20px !important;
              cursor: pointer;
            "
            @mouseenter="conversa.showDropdown = !conversa.showDropdown"
            @mouseleave="conversa.showDropdown = !conversa.showDropdown"
          >
            <div>
              <b-avatar variant="info" :src="avatarImg" size="4rem"></b-avatar>
            </div>
            <div style="flex-basis: 75%">
              <h6 class="m-0">{{ conversa.nome }}</h6>
              <p class="preview">
                {{ conversa.ultimaMsg }}
              </p>
            </div>
            <div class="d-flex flex-column align-items-center">
              <p class="m-0">{{ conversa.horario }}</p>
              <div class="d-flex align-items-center">
                <b-avatar
                  :text="conversa.notificacao"
                  size="18px"
                  style="background: #054d86; color: #fff"
                ></b-avatar>
                <b-dropdown
                  size="md"
                  variant="link"
                  toggle-class="text-decoration-none"
                  v-if="conversa.showDropdown"
                >
                  <b-dropdown-item
                    ><b-icon icon="pin"></b-icon> Fixar no topo</b-dropdown-item
                  >
                  <b-dropdown-item
                    ><b-icon icon="trash"></b-icon> Encerrar
                    conversa</b-dropdown-item
                  >
                </b-dropdown>
              </div>
            </div>
          </div>
        </b-tab>

        <b-tab>
          <template #title> <b-icon icon="alarm"></b-icon> Em espera </template>
          <p class="p-3">Tab contents 1</p>
        </b-tab>

        <b-tab>
          <template #title>
            <b-icon icon="person-circle"></b-icon> Contatos
          </template>
          <p class="p-3">Tab contents 1</p>
        </b-tab>

        <b-tab>
          <template #title>
            <b-icon icon="inboxes"></b-icon> Chat interno
          </template>
          <p class="p-3">Tab contents 1</p>
        </b-tab>
      </b-tabs>
    </v-flex>
    <v-flex lg9 class="p-0" style="overflow: hidden !important">
      <div class="noChat" v-if="!chatOpen"></div>
      <div v-else class="p-0 bg-light p-0 chat">
        <div
          class="d-flex align-items-center justify-content-between p-3"
          style="background: #fff; cursor: pointer"
          @click="infoOpen = !infoOpen"
        >
          <div class="d-flex align-items-center gap-2">
            <b-avatar :src="avatarImg" size="4rem"></b-avatar>
            <div>
              <h6 class="m-1">Wanderley</h6>
              <p>
                <b-icon icon="lightning-charge-fill"></b-icon> Conexão
                <b-icon icon="building"></b-icon> departamento
                <b-icon icon="person"></b-icon> Usuário
              </p>
            </div>
          </div>
          <div class="button d-flex gap-2">
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="search"></b-icon>
              <span> Buscar</span>
            </b-button>
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="file-text"></b-icon>
              <span> Notas</span>
            </b-button>
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="chat-right-dots-fill"></b-icon>
              <span> Mensagens agendadas</span>
            </b-button>
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="clock-history"></b-icon>
              <span> Histórico</span>
            </b-button>
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="plug-fill"></b-icon>
              <span> Teste</span>
            </b-button>
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="funnel-fill"></b-icon>
              <span> Funil</span>
            </b-button>
            <b-button class="buttonNavchat" variant="transparent">
              <b-icon icon="arrow-left-right"></b-icon>
              <span> Transferir</span>
            </b-button>
            <b-button
              variant="danger"
              style="color: #fff; box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25)"
            >
              <b-icon icon="telephone-x-fill"></b-icon>
              <span></span> Finalizar chamado
            </b-button>
          </div>
        </div>
        <div class="d-flex">
          <div
            class="lowChat"
            :style="infoOpen ? 'flex-basis: 75%' : 'flex-basis: 100%'"
          >
            <div class="messageContainer">
              <div
                v-for="mensagem in mensagens"
                :key="mensagem.id"
                :class="mensagem.enviada ? 'enviada' : 'recebida'"
                style="margin-bottom: 10px"
              >
                <p class="m-0">{{ mensagem.texto }}</p>
                <p
                  class="m-0"
                  style="text-align: right"
                  :style="
                    mensagem.enviada ? 'color: #e7e7e7' : 'color: #676767'
                  "
                >
                  {{ mensagem.hora }}
                </p>
              </div>
            </div>
            <div class="chatPainel">
              <b-button variant="primary">
                <b-icon
                  icon="paperclip"
                  style="color: #fff"
                  rotate="40"
                ></b-icon>
              </b-button>
              <b-button variant="primary">
                <b-icon icon="emoji-smile" style="color: #fff"></b-icon>
              </b-button>
              <b-form-input
                placeholder="Mensagem..."
                v-model="message"
              ></b-form-input>
              <b-button variant="primary" v-if="message">
                <b-icon icon="cursor" style="color: #fff"></b-icon>
              </b-button>
              <b-button variant="primary" v-else>
                <b-icon icon="mic" style="color: #fff"></b-icon>
              </b-button>
            </div>
          </div>
          <div
            class="p-2"
            style="
              overflow-y: scroll;
              background: #fff;
              height: 91.5vh;
              overflow-x: hidden;
            "
            :style="infoOpen ? 'flex-basis: 25%' : 'flex-basis: 0;'"
          >
            <div>
              <div>
                <b-icon
                  icon="x-lg"
                  @click="infoOpen = false"
                  style="cursor: pointer"
                ></b-icon>
              </div>
              <div class="d-flex flex-column align-items-center">
                <b-avatar :src="avatarImg" size="10rem"></b-avatar>
                <b-button
                  variant="transparent"
                  pill
                  class="bg-light"
                  style="color: #054d86; margin-top: -20px; margin-left: 90px"
                >
                  <b-icon icon="pencil"></b-icon>
                </b-button>
                <h2 class="m-0">Wanderley</h2>
                <p><b-icon icon="phone-fill"></b-icon> (84) 99999-8888</p>
              </div>
              <div
                class="p-2"
                style="border-top: 1px solid #e7e7e7; margin-top: 15px"
              >
                <h5><b-icon icon="tags-fill"></b-icon> Tags</h5>
                <b-form-input size="sm" placeholder="Selecione..." class="mt-1">
                </b-form-input>
                <div class="d-flex gap-2 mt-2">
                  <p class="p-1 rounded" style="background: red">Tag 1</p>
                  <p class="p-1 rounded" style="background: yellow">Tag 2</p>
                  <p class="p-1 rounded" style="background: green">Tag 3</p>
                </div>
              </div>
              <div
                class="p-2"
                style="border-top: 1px solid #e7e7e7; margin-top: 15px"
              >
                <h5><b-icon icon="person-fill"></b-icon> Atendente padrão</h5>
                <b-form-input size="sm" placeholder="Selecione..." class="mt-1">
                </b-form-input>
              </div>
              <div
                class="p-2"
                style="border-top: 1px solid #e7e7e7; margin-top: 15px"
              >
                <h5><b-icon icon="pencil-square"></b-icon> Observação</h5>
                <b-form-textarea size="sm" placeholder=""> </b-form-textarea>
              </div>
              <div
                class="p-2"
                style="border-top: 1px solid #e7e7e7; margin-top: 15px"
              >
                <h5><b-icon icon="hash"></b-icon> Protocolo de atendimento</h5>
                <p>78652345 <b-icon icon="clipboard"></b-icon></p>
              </div>
              <div
                class="p-2"
                style="border-top: 1px solid #e7e7e7; margin-top: 15px"
              >
                <h5>
                  <b-icon icon="info-circle"></b-icon> Campos personalizados
                </h5>
                <div
                  v-for="campoShow in camposPersonalizados"
                  :key="campoShow.id"
                  style="white-space: wrap"
                >
                  <p v-if="campoShow.nome != undefined">
                    <b>{{ campoShow.nome }}</b
                    >: {{ campoShow.valor }}
                  </p>
                </div>
                <b-button
                  @click="$bvModal.show('modalCamposPersonalizados')"
                  class="buttonNavchat"
                  variant="transparent"
                >
                  <b-icon icon="plus"></b-icon>
                  <span> Adicionar</span>
                </b-button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </v-flex>

    <!-- SideBar do usuario logado -->
    <b-sidebar id="sidebarUserInfo" left backdrop width="25%" shadow>
      <div class="px-3 py-2 d-flex flex-column align-items-center">
        <b-avatar :src="avatarImg" size="9rem"></b-avatar>
        <h4>Atendente 1</h4>
        <p>Departamento</p>
        <h5>4.6 <b-icon icon="star-fill" style="color: #054d86"></b-icon></h5>
      </div>
      <div>
        <button class="btnSideMenu">
          <b-icon icon="box-arrow-up-right"></b-icon> Atalhos
        </button>
        <button class="btnSideMenu">
          <b-icon icon="clock-history"></b-icon> Historico
        </button>
        <button class="btnSideMenu">
          <b-icon icon="chat-left-quote"></b-icon> Mensagens de ausência
        </button>
        <button class="btnSideMenu">
          <b-icon icon="chat-right-dots"></b-icon> Mensagens agendadas
        </button>
        <button class="btnSideMenu">
          <b-icon icon="lock"></b-icon> Mudar senha
        </button>
        <button class="btnSideMenu">
          <b-icon icon="door-open"></b-icon> Sair
        </button>
      </div>
    </b-sidebar>

    <!-- Modal campo personalizado -->

    <b-modal id="modalCamposPersonalizados" size="lg">
      <template #modal-header="{ close }">
        <b-button size="sm" variant="outline-danger" @click="close()">
          <b-icon icon="x"></b-icon>
        </b-button>
      </template>

      <div
        class="campos d-flex gap-2 mb-2"
        v-for="(campo, index) in camposPersonalizados"
        :key="campo.id"
      >
        <b-form-input placeholder="Nome" v-model="campo.nome"></b-form-input>
        <b-form-input placeholder="Valor" v-model="campo.valor"></b-form-input>
        <b-button variant="outline-danger" @click="removeCampo(index)">
          <b-icon icon="trash"></b-icon>
        </b-button>
      </div>
      <p v-if="camposPersonalizados.length == 0">
        Não há nenhum campo personalizado cadastrado.
      </p>
      <b-button
        variant="primary"
        style="color: #fff"
        class="mt-2"
        @click="addCampo"
      >
        <b-icon icon="plus"></b-icon> Adicionar
      </b-button>
      <template #modal-footer="{ ok }">
        <b-button
          size="sm"
          variant="primary"
          style="color: #fff !important"
          @click="ok()"
        >
          OK
        </b-button>
      </template>
    </b-modal>
  </v-layout>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    message: undefined,
    chatOpen: true,
    infoOpen: true,
    avatarImg: "http://www.colatina.es.gov.br/helpdesk/images/no-image.png",
    camposPersonalizados: [
      { id: Math.random(), nome: undefined, valor: undefined },
    ],
    conversas: [
      {
        id: Math.random(),
        nome: "Pedro",
        ultimaMsg:
          "Ola tudo bem jasdnflkjasdnflakjsdnflakjsdnfalkjsdnfalksjdnfaslkdjfnaskldfjn",
        horario: "17:00",
        notificacao: "3",
        showDropdown: false,
      },
      {
        id: Math.random(),
        nome: "Wanderley",
        ultimaMsg:
          "Ola tudo bem jasdnflkjasdnflakjsdnflakjsdnfalkjsdnfalksjdnfaslkdjfnaskldfjn",
        horario: "17:00",
        notificacao: "3",
        showDropdown: false,
      },
      {
        id: Math.random(),
        nome: "André",
        ultimaMsg:
          "Ola tudo bem jasdnflkjasdnflakjsdnflakjsdnfalkjsdnfalksjdnfaslkdjfnaskldfjn",
        horario: "17:00",
        notificacao: "3",
        showDropdown: false,
      },
    ],
    mensagens: [
      {
        id: Math.random(),
        texto:
          "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
        enviada: true,
        hora: "18:56",
      },
      {
        id: Math.random(),
        texto:
          "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
        enviada: false,
        hora: "18:56",
      },
    ],
  }),
  methods: {
    addCampo() {
      this.camposPersonalizados.push({
        id: Math.random(),
        nome: undefined,
        valor: undefined,
      });
    },
    removeCampo(pos) {
      this.camposPersonalizados.splice(pos, 1);
    },
  },
};
</script>
<style>
html {
  overflow-y: auto !important;
  font-size: 0.8rem !important;
}
html::-webkit-scrollbar {
  width: 8px;
}
html::-webkit-scrollbar-thumb {
  background: rgb(133, 133, 133);
}
.preview {
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 300px;
  white-space: nowrap;
}
.noChat {
  height: 100vh;
  background-image: url("./assets/logoClick.png");
  background-position: 50% 50%;
}
.btnSideMenu {
  color: #054d86;
  padding: 10px;
  font-size: 1.2rem;
  width: 100%;
  display: block;
  transition: 0.3s;
  border-top: 1px solid #e7e7e7;
}
.btnSideMenu:last-child {
  border-bottom: 1px solid #e7e7e7;
}
.btnSideMenu:hover {
  background: #054d86;
  color: #fff;
}
.buttonNavchat {
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  background: #fff !important;
  color: #054d86 !important;
  max-width: 38px;
  white-space: nowrap;
  overflow: hidden;
  transition: 0.7s !important;
}
.buttonNavchat span {
  visibility: hidden;
  transition: 0.7s;
}
.buttonNavchat:hover {
  max-width: 200px;
  border: none !important;
}
.buttonNavchat:hover span {
  visibility: visible;
}
.chat {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.enviada {
  background: #009aff;
  border-radius: 10px 20px 10px 20px;
  padding: 5px;
  max-width: 30%;
  color: #fff;
  align-self: flex-end;
}
.recebida {
  background: #9dd7ff;
  border-radius: 20px 10px 20px 10px;
  padding: 5px;
  max-width: 30%;
  align-self: flex-start;
}
.messageContainer {
  display: flex;
  flex-direction: column-reverse;
  width: 100% !important;
  padding: 10px 20px;
}
.chatPainel {
  display: flex;
  align-items: center;
  padding: 10px 20px;
  background: #fff;
  gap: 1rem;
  width: 100%;
}
.lowChat {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}
.novoCtt {
  position: absolute;
  z-index: 99;
  top: 85%;
  left: 1%;
  max-width: 50px;
  background: #054d86 !important;
  color: #fff !important;
}
@media (max-width: 1440px) {
  html {
    overflow-y: auto !important;
    font-size: 0.68rem;
  }
}
</style>
