<template lang="">
  <div class="category">
    <div class="category-buttons">
      <button @click="newsko" :class="{ active: activeCategory === '' }">전체</button>
      <button @click="news2('politics')" :class="{ active: activeCategory === 'politics' }">정치</button>
      <button @click="news2('economy')" :class="{ active: activeCategory === 'economy' }">경제</button>
      <button @click="news2('society')" :class="{ active: activeCategory === 'society' }">사회</button>
      <button @click="news2('culture')" :class="{ active: activeCategory === 'culture' }">문화</button>
      <button @click="news2('world')" :class="{ active: activeCategory === 'world' }">세계</button>
      <!-- <button @click="news2('entertainment')" :class="{ active: activeCategory === 'entertainment' }">Ent</button> -->
    </div>
  </div>

  <div v-for="handle in data" :key="handle.id" class="global-news">
    <div class="topkeyword">
      <h4 class="keyword">{{ getKoreanKeyword(handle.sections[0]) }}</h4>
      <p>{{ formatDate(handle.published_at) }}</p>
    </div>

    <img v-if="handle.image_url" :src="handle.image_url" />
    <img v-else :src="'/mainimg.png'" />

    <div class="title">
      <h2>📢</h2>
      <h2>{{ handle.title }}</h2>
    </div>

    <div class="moreText">
      <p :class="['summary', { hidden: handle.showMore }]">
        {{ handle.summary }}
      </p>
      <button class="more" @click="toggleSummary(handle)">
        <img :src="'/more.svg'" />
      </button>
    </div>
  </div>
  <p />
</template>

<script>
import axios from "axios";

export default {
  name: "NewsGlobal",
  data() {
    return {
      titleData: "",
      data: [],
      activeCategory: "", // 현재 활성 카테고리
    };
  },
  created() {
    this.newsko(); // 기본적으로 전체 뉴스 로드
  },
  methods: {
    async newsko() {
      this.activeCategory = ""; // 전체 카테고리 활성화
      try {
        const api = await axios.get(`https://server-woad-theta.vercel.app/news/ko`);
        this.titleData = api.data.data[0].title;
        this.data = api.data.data.map((handle) => ({
          ...handle,
          showMore: false,

        }));
        console.log(api);
      } catch (error) {
        console.error("Error fetching news:", error);
      }
    },
    async news2(category) {
      this.activeCategory = category; // 선택한 카테고리 활성화
      try {
        const api = await axios.get(
          `https://server-woad-theta.vercel.app/news/categoryko?category=${category}`
        );

        this.data = api.data.data.map((handle) => ({
          ...handle,
          showMore: false,
        }));
      } catch (error) {
        console.error("Error fetching news:", error);
      }
    },
    getKoreanKeyword(keyword) {
      const keywords = {
        society: "사회",
        politics: "정치",
        economy: "경제",
        culture: "문화",
        technology: "기술",
        entertainment: "엔터테인먼트",
        sports: "스포츠",
        world:"세계",
      };
      return keywords[keyword] || keyword;
    },
    formatDate(dateString) {
      const date = new Date(dateString);
      const year = date.getFullYear();
      const month = date.getMonth() + 1;
      const day = date.getDate();
      const hours = date.getHours();
      const minutes = date.getMinutes();
      return `${year}년 ${month}월 ${day}일 ${hours}시 ${minutes}분`;
    },
    toggleSummary(handle) {
      handle.showMore = !handle.showMore;
    },
  },
};
</script>

<style lang="scss">
body {
  max-width: 480px;
  margin: 0 auto;
  overflow-x: hidden;
}

.category {
  padding-bottom: 15px;
  display: flex;
  justify-content: space-around;
  align-items: center;

  .category-buttons {
    display: flex;
    justify-content: space-around;
    width: 100%;

    button {
      width: 70px;
      height: 50px;
      font-size: 16px;    
      padding: 10px;
      gap: 10px;
      background-color: transparent;
      border: none;
      border-bottom: solid 2px transparent; // 기본 보더 설정
      transition: border-color 0.3s ease, color 0.5s ease; // 트랜지션 추가

      &.active {
        border-bottom: solid 2px #458FFF; // 활성화된 버튼의 하단 보더
        color: #458FFF; // 활성화된 버튼 색상
        font-weight: 700;
      }
    }
  }
}

.global-news {
  width: auto;
  border-radius: 10px;
  margin-bottom: 50px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  padding: 14px 24px;

  &:hover {
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
  }

  .topkeyword {
    display: flex;
    justify-content: space-between;
    align-items: center;

    p {
      font-size: 14px;
      color: #767676;
    }
  }

  .keyword {
    width: 130px;
    padding: 5px;
    border-radius: 20px;
    border: solid 1px #000;
    margin-left: 10px;
  }

  .title {
    display: flex;
    width: 95%;
    text-align: left;
    margin-left: 10px;
    align-items: baseline;
    color: #2b2b2b;

    h2:nth-child(1) {
      width: 40px;
    }

    h2:nth-child(2) {
      display: -webkit-box;
      -webkit-box-orient: left;
      -webkit-line-clamp: 2;
      text-overflow: ellipsis;
      margin: 5px 0px 0px;
    }
  }

  .summary {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 4;
    overflow: hidden;
    text-overflow: ellipsis;
    margin: 10px 0px 10px;
    margin-left: 10px;
    text-align: left;
  }

  .hidden {
    display: block; // 숨김 클래스
  }

  img {
    max-width: 100%;
    height: 300px;
    object-fit: cover;
  }

  .more {
    width: 100%;
    height: 50px;
    border: solid 0px;
    background-color: transparent;

    img {
      height: 50px;
    }
  }
}
</style>
