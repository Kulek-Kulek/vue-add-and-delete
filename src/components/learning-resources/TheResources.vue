<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResBtnMode"
      >Stored resources</base-button
    >
    <base-button @click="setSelectedTab('add-resource')" :mode="addResBtnMode"
      >Add resource</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'This is an official guide and description of Vue.js',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          describtion: 'Learn to google!!!!',
          link: 'https://google.org',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
    };
  },
  computed: {
    storedResBtnMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResBtnMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, describtion, link) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        describtion,
        link,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const index = this.storedResources.findIndex(
        (resource) => resource.id === resId
      );
      this.storedResources.splice(index, 1);
    },
  },
};
</script>
