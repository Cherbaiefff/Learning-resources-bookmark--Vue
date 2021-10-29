<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResBtnMode"
    >
      Stored Resource
    </base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addResBtnMode">
      Add Resource
    </base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
  name: 'TheResource',
  components: {
    AddResource,
    StoredResources
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com'
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addNewResource: this.addNewResource,
      removeResource: this.removeResource
    };
  },
  computed: {
    storedResBtnMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResBtnMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addNewResource(title, description, link) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        description,
        link
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resourceIdx = this.storedResources.findIndex(
        res => (res.id = resId)
      );
      this.storedResources.splice(resourceIdx, 1);
    }
  }
};
</script>
