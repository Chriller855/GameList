<template>
  <v-container class="grey lighten-5">
    <v-toolbar dark>
      <v-menu offset-y>
        <template v-slot:activator="{ on, attrs }">
          <v-btn Icon v-bind="attrs" v-on="on">
            <v-icon>mdi-menu</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item>
            <v-btn icon>
              <v-icon>mdi-view-grid</v-icon>
            </v-btn>
            <v-btn icon>
              <v-icon>mdi-view-sequential</v-icon>
            </v-btn>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-text-field hide-details append-icon="mdi-magnify" single-line v-model="search"></v-text-field>
    </v-toolbar>
    <v-row>
      <v-col v-for="(item, i) in filteredList" :key="i" cols="12" xs="12" sm="12" md="6" lg="4">
        <v-card dark >
          <div class="flex-no-wrap flex-grow-1 justify-space-between">
            <div class="d-flex">
              <div>
                <v-card-title class="headline" v-text="item.title"></v-card-title>
                <v-card-subtitle v-text="'Jackpot ' + item.jackpot"></v-card-subtitle>
              </div>
              <v-spacer></v-spacer>
              <v-avatar class="ma-3" size="140" tile>
                <v-img :src="item.picture" style="position: absolute;"></v-img> <!-- Remove InlineStyle -->
                <v-img :src="'https://www.spilnu.dk/uploads/combined_games/'+item.pictureId+'/large_gametile.jpg'" style="position: absolute;"></v-img>
                <v-img :src="'https://www.spilnu.dk//uploads/combined_games/'+item.pictureId+'/large_gamelogo.png'" contain style="position: absolute;"></v-img>
              </v-avatar>
            </div>
            <v-card-subtitle v-show="item === itemToShow" v-text="item.description"></v-card-subtitle>
            <v-card-text>
              <v-chip-group active-class="deep-purple accent-4 white--text" column>
                <v-chip v-for="(tag, i) in item.tags" :key="i" v-text="tag"></v-chip>
              </v-chip-group>
             Created {{item.created}}
            </v-card-text>
            <div class="d-flex">
              <v-btn class="ml-2 mt-5 success" outlined rounded >Play</v-btn>
              <v-spacer></v-spacer>
              <v-btn class="ml-2 mt-5" outlined rounded v-on:click="moreClick(item)">
                <div v-if="item === itemToShow">Less</div>
                <div v-else>More</div>
              </v-btn>
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

export default {
  name: "game-list",
  computed: {
    filteredList() {
      return this.items.filter(game => {
        return (
          game.title
            .toLowerCase()
            .includes(this.search.toLowerCase()) ||
          game.tags
            .toString()
            .toLowerCase()
            .includes(this.search.toLowerCase())
        );
      });
    }
  },
  methods: {
    moreClick: function(item) {
      if (this.itemToShow === item) {
        this.itemToShow = null;
      } else {
        this.itemToShow = item;
      }
    }
  },
  data: () => ({
    search: '',
    itemToShow: null,
    items: [ // Should be Inported Not inserted
      {
        id: "5ab26f6b16153424d64cf669",
        index: 0,
        hot: false,
        jackpot: "$2,274.02",
        picture: "http://placehold.it/500x500",
        pictureId: 172,
        title: "Heidi Hunt",
        description:
          "Commodo aute excepteur consequat officia sunt dolor laboris qui minim tempor adipisicing. Do id voluptate exercitation duis aute. Deserunt fugiat qui do aute proident tempor do nulla et ex. Occaecat sint velit excepteur et. Minim ad tempor dolor non sint sit dolor id dolor.\n\nLorem labore culpa cillum non ea occaecat tempor laboris. Cillum consequat ea sit aute. Ea non non eiusmod et aliquip labore eiusmod.",
        created: "04/13/2015",
        tags: ["proident", "nulla", "excepteur", "adipisicing", "reprehenderit"]
      },
      {
        id: "5ab26f6b62406eed4cf29da1",
        index: 1,
        hot: false,
        jackpot: "$2,477.67",
        picture: "http://placehold.it/500x500",
        pictureId: 168,
        title: "Diamond Express",
        description:
          "Occaecat eu ad amet dolor elit. Velit aliqua ipsum ipsum dolore quis pariatur Lorem quis ex Lorem non minim magna. Lorem ullamco aliquip eu aliquip aute labore deserunt sit ipsum nisi esse.\n\nLaborum amet labore veniam ea aliquip quis eu. Ea nostrud irure enim nostrud sit reprehenderit in. Proident laboris adipisicing qui reprehenderit magna deserunt in anim ad aute. In velit deserunt esse nisi. Proident tempor occaecat aute et.",
        created: "01/22/2014",
        tags: ["non", "aliqua", "adipisicing", "excepteur", "irure"]
      },
      {
        id: "5ab26f6b71affd6e32ad3fb6",
        index: 2,
        hot: true,
        jackpot: "$2,658.04",
        picture: "http://placehold.it/500x500",
        pictureId: 173,
        title: "Jewel Heist",
        description:
          "Mollit tempor ullamco anim ad et irure minim. Laboris ex quis labore anim ipsum esse ullamco excepteur ea incididunt. Tempor laboris pariatur magna sit cillum duis esse eiusmod mollit sunt proident. Exercitation ullamco proident incididunt reprehenderit ad culpa dolor anim ullamco commodo voluptate irure. Non quis ut anim veniam velit qui est qui. Consequat ea ut esse commodo eiusmod aliquip excepteur est dolore voluptate fugiat exercitation eu cillum.\n\nNon velit commodo cillum laborum nisi reprehenderit elit cillum ad consequat aliquip fugiat. Laboris esse fugiat est cillum aute nostrud laboris duis mollit deserunt minim ad aliqua incididunt. Proident fugiat aliquip elit velit ullamco sunt sit sint esse cillum. Ex consectetur et reprehenderit elit nostrud consectetur do adipisicing. Nulla commodo cillum laborum do commodo in.",
        created: "08/21/2017",
        tags: ["esse", "elit", "officia", "consectetur", "amet"]
      },
      {
        id: "5ab26f6b01b851aae575e029",
        index: 3,
        hot: true,
        jackpot: "$2,578.56",
        picture: "http://placehold.it/500x500",
        title: "Stone Age",
        description:
          "Nulla duis minim ipsum mollit fugiat. Cupidatat deserunt qui id velit voluptate voluptate ex amet nostrud laborum. Aliquip incididunt non pariatur ipsum velit. Cillum exercitation labore exercitation fugiat ut elit.\n\nCillum non sit ex consequat eiusmod. Pariatur esse excepteur in elit sunt ullamco cupidatat amet occaecat aute qui commodo consequat labore. Tempor est est eiusmod sit laborum dolore amet officia qui. Culpa dolor ad ullamco minim amet sunt. Fugiat laborum commodo veniam sint dolor magna. Excepteur officia deserunt ipsum sunt ipsum consectetur elit qui nostrud minim ipsum proident exercitation nostrud.",
        created: "01/17/2016",
        tags: ["mollit", "labore", "et", "ipsum", "consectetur"]
      },
      {
        id: "5ab26f6bd5d24cb5f07610c4",
        index: 4,
        hot: true,
        jackpot: "$1,887.20",
        picture: "http://placehold.it/500x500",
        pictureId: 169,
        title: "Fish Tank",
        description:
          "Veniam non ut ad est Lorem eu duis esse anim sint. Nulla ullamco excepteur occaecat amet velit adipisicing reprehenderit nisi. Nulla in ex quis mollit. Ut aliquip id fugiat deserunt nostrud culpa irure pariatur duis excepteur consectetur. Aute qui ex consequat excepteur dolor laboris laborum duis. Pariatur aliquip commodo veniam irure voluptate irure minim commodo non proident non.\n\nQui esse duis ex qui fugiat irure labore adipisicing. Aliquip culpa Lorem labore qui sint. Fugiat tempor aute sit minim. Tempor aute eu velit commodo labore. Laborum officia ullamco ex sint nostrud consectetur aliqua enim nostrud qui qui incididunt.",
        created: "05/10/2016",
        tags: ["elit", "voluptate", "nisi", "velit", "anim"]
      },
      {
        id: "5ab26f6b506b63cdf4957dce",
        index: 5,
        hot: false,
        jackpot: "$3,641.62",
        picture: "http://placehold.it/500x500",
        title: "Golden Pyramid",
        description:
          "Eiusmod exercitation magna id ad esse aliqua nulla proident sit. Pariatur laborum elit irure id deserunt sint sint ad irure. Incididunt cupidatat esse do ipsum dolor anim irure. Deserunt commodo laboris non elit ad laboris ea nostrud est ex ipsum nulla aute ullamco. Velit proident ad tempor aliqua magna occaecat elit veniam cillum mollit fugiat.\n\nSint laboris ipsum aute cupidatat laboris elit excepteur. Eu aliquip non cillum exercitation laborum anim nulla dolore non. Et est duis in in in incididunt reprehenderit minim non Lorem. Aute minim culpa laboris commodo do tempor cillum occaecat reprehenderit excepteur amet. Duis proident qui excepteur ut laborum eu elit tempor proident amet. Non sint pariatur sit fugiat duis elit voluptate ut velit ipsum labore id aliqua excepteur.",
        created: "06/07/2014",
        tags: ["eu", "mollit", "commodo", "adipisicing", "esse"]
      },
      {
        id: "5ab26f6b87c8a0dac830ae6c",
        index: 6,
        hot: false,
        jackpot: "$1,961.37",
        picture: "http://placehold.it/500x500",
        pictureId: 167,
        title: "Deep Blue",
        description:
          "Commodo Lorem nulla duis amet amet ut voluptate commodo veniam do pariatur. Enim culpa pariatur esse est ad in pariatur exercitation et. Officia occaecat proident nostrud tempor sunt. Cupidatat ad duis do sit magna nostrud enim enim. Consectetur ut Lorem sit id amet irure ea aliqua. Adipisicing enim proident elit cupidatat duis consectetur. Tempor ea commodo proident ullamco id eiusmod ut aute.\n\nCommodo aliqua sint mollit et ullamco incididunt irure nisi minim aute in ex id esse. Aliquip sint incididunt adipisicing ipsum pariatur sit ad sit enim dolore elit veniam. Eiusmod in elit aliqua sunt sit quis esse mollit laborum esse commodo magna.",
        created: "05/31/2016",
        tags: ["ad", "id", "ut", "eiusmod", "pariatur"]
      },
      {
        id: "5ab26f6b88a46d0899f51e49",
        index: 7,
        hot: true,
        jackpot: "$2,840.35",
        picture: "http://placehold.it/500x500",
        pictureId: 163,
        title: "Inspector",
        description:
          "Consectetur duis incididunt veniam ex ex incididunt. Magna ut sit occaecat eu officia id. Non aute nostrud minim tempor eiusmod fugiat aute consectetur non sint proident aliqua. Exercitation anim pariatur fugiat incididunt adipisicing in id incididunt fugiat laboris.\n\nEa proident aliqua consectetur ex sit ea ea officia commodo commodo pariatur esse. Eu quis ullamco ullamco proident non eu ex esse proident veniam irure dolore sint. Eu cupidatat irure est eiusmod enim tempor Lorem est incididunt fugiat magna labore sit. Eiusmod anim sunt exercitation consequat.",
        created: "01/12/2016",
        tags: ["ad", "sunt", "ipsum", "qui", "labore"]
      }
    ]
  })
};
</script>

