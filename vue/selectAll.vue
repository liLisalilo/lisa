<script src="http://cdnjs.cloudflare.com/ajax/libs/vue/1.0.7/vue.min.js"></script>
<div id="app">
    <div v-for="list in lists">
        <div class="row">
            <div class="col-sm-12">
                <div class="checkbox">
                    <label>
                        <input type="checkbox" @change="toggleSelect(list)" v-model="list.checked">
                        <strong class="">{{list.name}}</strong>
                    </label>
                </div>
            </div>
        </div>
        <div class="row" style="margin-left: 10px;">
            <div class="col-sm-offset-1 col-sm-11" v-for="permission in list.permissions">
                <div class="checkbox">
                    <label>
                        <input type="checkbox"  :value="permission.id" v-model="permission.checked" @change="handle(list)">
                        <span class="">{{permission.display_name}}</span>
                        <span class="text-muted ">- {{permission.description}}</span>
                        &nbsp;
                        <span class="text-danger "></span>
                    </label>
                </div>
            </div>
        </div>
    </div>
    <div>
        <strong>选中id：</strong>
        <i v-for="permission in permissions">{{permission}}  </i>
    </div>
</div>
<!--vue2.1.10, vue1不行-->
<script>
new Vue({
  el: '#app',
  data: {
    lists: [
  {
    "id": 1,
    "name": "Member",
    "checked": false,
    permissions: [
      {
        "display_name": "Reset withdraw password",
        "id": 10,
        "checked": false,
        "description": "Can reset member’s withdraw password."
      },
      {
        "display_name": "Reset password",
        "id": 9,
        "checked": false,
        "description": "Can reset member's password"
      },
      {
        "display_name": "Bank account detail management",
        "id": 8,
        "checked": false,
        "description": "Can list and modify the data of member's bank."
      }
    ]
  },
  {
    "id": 2,
    "name": "Agent",
    "checked": false,
    permissions: [
      {
        "display_name": "Update “大股東”(Agent level = 1) detail",
        "id": 7,
        "checked": false,
        "description": "Can modify level 1 agent’s data."
      },
      {
        "display_name": "Update “大股東”(Agent level = 2) detail",
        "id": 6,"checked": false,
        "description": "Can modify level 2 agent’s data."
      },
      {
        "display_name": "Update “大股東”(Agent level = 3) detail",
        "id": 5,"checked": false,
        "description": "Can modify level 3 agent’s data."
      },
      {
        "display_name": "Update “大股東”(Agent level = 4) detail",
        "id": 4,"checked": false,
        "description": "Can modify level 4 agent’s data."
      }
    ]
  },
  {
    "id": 3,
    "checked": false,
    "name": "Transaction",
    permissions: [
      {
        "display_name": "View remit, online and withdraw",
        "id": 3,"checked": false,
        "description": "Can view remit, online and withdraw page."
      },
      {
        "display_name": "Transaction permit",
        "id": 2,"checked": false,
        "description": "Can approve remit, online and withdraw. Can update auditing"
      },
      {
        "display_name": "Decline payment",
        "id": 1,"checked": false,
        "description": "Can decline payment"
      }
    ]
  }],
    permissions: []
    },
      methods: {
        handle: function(list) {
            list.checked = list.permissions.every(function(permission){
              return permission.checked;
            })
          this.getSelect ()
        },
        toggleSelect: function(list) {
          list.permissions.forEach(function(permission) {
                permission.checked = list.checked
          })
        this.getSelect ()
        },
        getSelect () {
            let selectId = []
            for (let list in this.lists) {
                for (let index in this.lists[list].permissions) {
                    if (this.lists[list].permissions[index].checked) {
                        selectId.push(this.lists[list].permissions[index].id)
                    }
                }
            }
            this.permissions = selectId
        }
      }
    })
</script>
