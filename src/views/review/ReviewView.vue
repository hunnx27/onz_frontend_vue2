<template>
  <!-- Wrap START -->
  <div class="review">
    <!-- 메인슬라이더 START -->
    <v-carousel
      :show-arrows="false"
      cycle
      height="250"
      hide-delimiter-background
      >
      <v-carousel-item v-for="(item,i) in sliedeitems" :key="i">
        <v-sheet
          height="100%"
          color="black"
          tile
        >
          <v-row
            class="fill-height slide-row"
            align="center"
            justify="center"
            :style="{backgroundImage:'url('+item.src+')'}"
          >
            <v-col cols="12" sm="12" md="12" class="text-center">
              <h1>{{item.name}}</h1>
              <div>
                <p>
                  원앤집 지표점수는?
                </p>
                <p>
                  {{item.score}}점
                </p>
              </div>
            </v-col>
          </v-row>
        </v-sheet>
      </v-carousel-item>
    </v-carousel>
    <!-- 메인슬라이더 END -->
    
    <!-- 메뉴 1,2 START -->
    <v-container class="pa-0">
      <v-row
        align="center"
        class="grey lighten-5 mb-6 ma-0"
        style="width:100%"
      >
        <v-col
          alilgn='start'
          no-gutters
        >
          <v-menu offset-y>
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                text
                v-bind="attrs"
                v-on="on"
              >
                {{selectedMenu1}} <v-icon>mdi-menu-down</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(item, index) in menu1Items"
                :key="index" @click="selectMenu1(item.title)"
              >
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </v-col>
        <v-col alilgn='center'/>
        <v-col
          alilgn='end'
          no-gutters
          style='text-align:right'
        >
          <v-btn text
            @click="dialog1 = true"
          >
            {{selectedMenu2}} <v-icon>mdi-menu-down</v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
    <!-- 메뉴 1,2 END -->

    <v-container>

      <!-- -->
      <v-row v-for="n in 20" :key="n">
        <v-col class="">
          <v-card
            class="mx-auto"
            width="100%"
          >
            <v-card-title>
              열린어린이집
            </v-card-title>
            <v-card-subtitle>
              > 가정 > 경기도 화성시
            </v-card-subtitle>
            <v-card-text>
              <div class="text--primary">
                애기 혼자놀다 다쳐도 교사탓 원장 참견심하고 교사컴퓨터1대로 3명돌아가면서 씀<br/>
                원장이 기분파라 기분 맞추기 힘듬
              </div>
            </v-card-text>
            <v-card-actions>
              <v-card
                class="mx-auto"
                width="100%"
              >
                <v-card-text>
                  <v-row>
                    <v-col><v-icon>mdi-face-man</v-icon><v-icon>mdi-cards-heart</v-icon><v-icon>mdi-cards-heart-outline</v-icon></v-col>
                    <v-col>총 만족도 : 5</v-col>
                    <v-col>업무량 : 4</v-col>
                    <v-col>원내분위기 : 3</v-col>
                  </v-row>
                </v-card-text>
              </v-card>
            </v-card-actions>
          </v-card>

        </v-col>
      </v-row>
    </v-container>

    <!-- dailog1 START -->
    <v-dialog
      v-model="dialog1"
      max-width="500px"
    >
      <v-card>
        <v-card-title>
          검색조건을 선택하세요.
        </v-card-title>
        <v-card-text>
          <v-radio-group row >
            <!--FIXME -->
            <v-radio label="전체" color="warning" value="all" ></v-radio>
            <!--FIXME -->
            <v-radio label="어린이집" color="warning" value="type1" ></v-radio>
            <!--FIXME -->
            <v-radio label="유치원" color="warning" value="type2" ></v-radio>
          </v-radio-group>
          <v-select
            :items="menu2_items1"
            label="유형"
            item-value="text"
          ></v-select>
          <v-row >
            <v-col>
              <v-select
                :items="menu2_items2"
                label="시/도"
                item-value="text"
              ></v-select>
            </v-col>
            <v-col>
              <v-select
                :items="menu2_items3"
                label="상세주소"
                item-value="text"
              ></v-select>
            </v-col>
          </v-row>
        </v-card-text>
        <v-card-actions text->
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog1 = false"
          >
            확인
          </v-btn>
          <v-btn
            color="primary"
            text
            @click="dialog1 = false"
          >
            취소
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <!-- dailog1 END -->

  </div>
  <!-- Wrap END -->

</template>

<style>
.v-carousel__controls{
  top:0
}
.slide-row{
  background-position: center;
  background-size: cover;
}
</style>
<script>
export default {
  name: 'ReviewItem',
  components:{
    
  },
  data(){
    return{
      selectedMenu1: '전체리뷰보기',
      selectedMenu2: '기관/지역순',
      dialog1: false,
      sliedeitems: [
        {
          id: 1,
          name: '송파유정유치원',
          score: 68,
          src: 'https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg',
        },
        {
          id: 2,
          name: '오창과학 미래어린이집',
          score: 52,
          src: 'https://cdn.vuetifyjs.com/images/carousel/sky.jpg',
        },
        {
          id: 3,
          name: '하나유치원',
          score: 44,
          src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg',
        },
      ],
      menu1Items: [
        { title: '전체리뷰보기' },
        { title: '기관리뷰만보기' },
        { title: '면접리뷰만보기' },
        { title: '연봉리뷰만보기' },
      ],
      menu2_items1:["전체", "국롱립", "사회복지법인"],
      menu2_items2:["전체", "서울특별시"],
      menu2_items3:["전체", "강남구"]
    }
  },
  methods:{
    selectMenu1(val){
      this.selectedMenu1 = val;
    },
    selectMenu2(val){
      this.selectedMenu2 = val;
    }
  }

}
</script>
