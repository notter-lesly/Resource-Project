<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode"
    >
      Stored Resources
    </base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">
      Add Resource
    </base-button>
  </base-card>
  <keep-alive>
  <component :is="selectedTab"> </component>
  </keep-alive>
</template>

<script>
import storedResources from './StoredResources.vue';
import addResource from './AddResource.vue';

export default {
  components: {
    storedResources,
    addResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official-guide',
          description: 'The official Vue-JS documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'You have to learn how to google',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url){
      const newResource = {
id: new Date().toISOString(),
title:title,
description:description,
link:url
      }
      this.storedResources.unshift(newResource)
      this.selectedTab = "stored-resources"
    },
    removeResource(resId){
  const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    }
  },
  computed:{
storedResButtonMode(){
  return this.selectedTab === 'stored-resources' ? null : 'flat'
},
addResButtonMode(){
  return this.selectedTab === 'add-resources' ? null : 'flat'
}

  }
};
</script>

<style scoped></style>
