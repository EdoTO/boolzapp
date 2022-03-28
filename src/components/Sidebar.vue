<template>

  <body>
      
      <div class="sidebar">

        <div class="sb__header">
            <span>BETA</span>
            <figure class="avatar">
                <img src="../img/avatar.png" alt="">
            </figure>
            <i class="fa-solid fa-circle-notch"></i>
            <i class="fa-solid fa-pen-to-square"></i>
            <i class="fa-solid fa-chevron-down"></i>
        </div>

        <div class="sb__searchbar">
            <div class="container">
                <i class="fa-solid fa-magnifying-glass"></i>
                <input type="text" placeholder="Cerca o inizia una nuova chat">
            </div>
        </div>

        <div class="sb__main">

          <div v-for="(element, i) in contacts" :key="i" @click="activeContact=element" class="item" :class="activeContact === element ? 'active' : ''">
              <div class="logo">
                  <img :src="element.avatar" :alt="element.avatar">
              </div>
              <div class="content">
                  <div class="details">
                      <span id="name">{{element.name}}</span>
                      <span id="last-message">{{element.text}}</span>
                  </div>
                  <div class="date">
                      <span>{{element.date}}</span>
                  </div>
              </div>             
            </div>

        </div>

    </div>

    <div class="chat">

      <div class="chat__header">
        <div class="data">

            <figure class="avatar">
                <img src="../img/avatar.png" alt="">
            </figure>

            <div class="identity">
                <h4>{{activeContact.name}}</h4>
                <span>{{activeContact.accesso}}</span>
            </div>
            
        </div>

        <div class="actions">
            <i class="fa-solid fa-video"></i>
            <i class="fa-solid fa-phone"></i>
            <span>|</span>
            <i class="fa-solid fa-magnifying-glass"></i>
            <i class="fa-solid fa-chevron-down"></i>
        </div>

      </div>

      <div class="chat__main">

          <div v-for="(element, i) in activeContact.messages" :key="i" :class="element.status" class="message">
              {{element.text}}
              <span class="message__date">{{ getHours(element.date) }}</span>
          </div>
          

      </div>

      <div class="chat__footer">

          <i class="fa-solid fa-face-smile"></i>
          <i class="fa-solid fa-paperclip"></i>
          <div>
              <input class="textbox" v-model="newMessage" @keyup.enter="send()" placeholder="  Scrivi un messaggio" type="text">
          </div>
          <i class="fa-solid fa-microphone"></i>
          <i class="fa-solid fa-paper-plane"></i>

      </div>

    </div>

  </body>

</template>

<script>

export default {
    name: 'Sidebar',
    data() {

        return {
            newMessage: '',
            activeContact: null,
            contacts: [
       {
          name: "Michele",
          accesso: "oggi alle 19:20",
          avatar: "../img/01.jpg",
          visible: true,
          messages: [
              {
                date: "15:30",
                text: "Hai portato a spasso il cane?",
                status: "sent",
                seen: "read",
            },
             {
                date: "15:50",
                text: "Ricordati di dargli da mangiare",
                status: "sent",
                seen: "read",
            },
            {
                date: "16:15",
                text: "Tutto fatto!",
                status: "received",
            },
        ],
    },
     {
        name: "Fabio",
        accesso: "oggi alle 18:30",
        avatar: "../img/02.webp",
        visible: true,
        messages: [
            {
                date: "16:30",
                text: "Ciao come stai?",
                status: "sent",
                seen: "read",
            },
            {
                date: "16:30",
                text: "Bene grazie! Stasera ci vediamo?",
                status: "received",
            },
            {
                date: "16:35",
                text: "Mi piacerebbe ma devo andare a fare la spesa.",
                status: "sent",
                seen: "unread",
            },
        ],
     },
     {
        name: "Samuele",
        accesso: "oggi alle 20:20",
        avatar: "../img/03.webp",
        visible: true,
        messages: [
             {
                date: "10:10",
                text: "La Marianna va in campagna",
                status: "received",
             },
             {
                 date: "10:20",
                 text: "Sicuro di non aver sbagliato chat?",
                 status: "sent",
                 seen: "read",
             },
             {
                 date: "16:15",
                text: "Ah scusa!",
                status: "received",
             },
        ],
    },
    {
        name: "Luisa",
        accesso: "oggi alle 17:20",
        avatar: "../img/04.jpg",
        visible: true,
        messages: [
             {
                 date: "15:30",
                text: "Lo sai che ha aperto una nuova pizzeria?",
                status: "sent",
                seen: "read",
            },
            {
                date: "15:50",
                text: "Si, ma preferirei andare al cinema",
                status: "received",
            },
        ],
     },     
   ],
}
  },
  methods: {
      selectContact: function(contact) {
        this.activeContact = contact;
    },

    getHours: function(date) {
        const hour = date;
        return hour;
    },
    send: function() {

        const message = this.createMessage(this.newMessage, 'sent');
        const index = this.activeContact;

        this.activeContact.messages.push(message);

        this.newMessage = '';

        setTimeout(() => {
            this.reply(index);
        }, 2000);
        
    },

    reply: function(index) {

        const message = this.createMessage('ricevuto', 'received');

        this.activeContact = index;
        this.activeContact.messages.push (message)



    },

    createMessage: function (text, status) {

        const date = new Date();
        const newMessage = {
            status: status,
            text: text,
            date: `${ date.getHours() }:${ date.getMinutes() }`
        }
        
        return newMessage;
    }
    
  },

  created() {
        this.selectContact(this.contacts[0])
    },
    
}
</script>

<style lang="scss" scoped>

    .sidebar > div {
        width: 100%;
        padding: 10px;
        display: flex;
        align-items: center;
    }

    .avatar img {
        width: 30px;
        border-radius: 50%;
    }

    .sidebar {

        border-right: 1px solid rgb(207, 207, 207);

        .sb__header {

            justify-content: flex-end;
            gap: 20px;
            background-color: rgb(238, 238, 238);

        }

        .sb__searchbar {

            
            .container {
                display: flex;
                align-items: center;
                gap: 20px;
                width: 100%;
                height: 30px;
                border: none;
                border-radius: 8px;
                background-color: rgb(228, 228, 228);
                padding: 10px;

                input {
                    background-color: rgb(228, 228, 228);
                    border: none;
                    flex-grow: 1;
                }
            }
        }

        .sb__main {
            display: flex;
            flex-direction: column;
            padding: 0 10px;

            .item:first-child {
                border-top: 1px solid lightgray;
            }

            .item.active {
                background-color: rgb(228, 228, 228)
            }

            .item {
                display: flex;
                gap: 20px;
                width: 100%;
                border-bottom: 1px solid lightgray;
                padding: 10px 0;

                .logo img{
                    width: 40px;
                    border-radius: 50%;
                    vertical-align: middle;
                }

                .content{
                    display: flex;
                    justify-content: space-between;
                    flex-grow: 1;
                    align-items: center;

                    .details {
                        display: flex;
                        flex-direction: column;
                        gap: 2px;

                        #name {
                            font-weight: 700;
                        }

                        #message {
                            font-size: 14px;
                        }
                        
                    }
                }
            }
        }

        
    }

    .chat {
        
        display: flex;
        flex-direction: column;


        .chat__header {
            width: 100%;
            height: 54px;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 20px;
            background-color: rgb(238, 238, 238);
            

            .data {

                display: flex;
                gap: 20px;
                align-items: center;

                .identity {
                    display: flex;
                    flex-direction: column;

                    span {
                        font-size: 14px;
                    }
                }
            }

            .actions {
                display: flex;
                gap: 20px;
                align-items: center;

                span {
                    font-size: 25px;
                }
            }
        }

        .chat__main{
            background-image: url('../img/boolzapp__bg.png');
            display: flex;
            flex-direction: column;
            gap: 10px;
            object-fit: cover;
            object-position: center;
            flex-grow: 1;
            padding: 40px;

            .message {
                border-radius: 8px;
                box-shadow: 0 2px 3px rgb(194, 194, 194);
                margin: -3px 0;
                padding: 10px 12px;
                max-width: 60%;
                position: relative;
            }

            .message__date {
                font-size: 12px;
                color: grey;
                position: relative;
                top: 8px;
                left: 4px;
            }

            .triangle-sent{
                width: 0;
                height: 0;
                position: absolute;
                top: 0;
                right: -10px;
                border-style: solid;
                border-width: 20px 20px 0 0;
                border-color: lightgreen transparent transparent transparent;
            }

            .triangle-received {
                width: 0;
                height: 0;
                position: absolute;
                top: 0;
                left: -10px;
                border-style: solid;
                border-width: 0 20px 20px 0;
                border-color: transparent white transparent transparent;
            }

            .message.sent + .message.received {
                margin-top: 2px
            }

            .message.received + .message.sent {
                margin-top: 2px
            }

            .sent {
                background-color: lightgreen;
                align-self: flex-end;
            }

            .received {
                background-color: white;
                align-self: flex-start;
            }

        }

        .chat__footer {
            padding: 10px 20px;
            background-color: rgb(238, 238, 238);
            display: flex;
            gap: 20px;
            align-items: center;

            i {
                font-size: 20px;
            }

            div {
                flex-grow: 1;

                .textbox {
                    width: 100%;
                    height: 35px;
                    border: none;
                    border-radius: 8px;
                    font-size: 20px;
                }
            }
        }
    }



</style>