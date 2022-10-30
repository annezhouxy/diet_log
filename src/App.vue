<template>
  <!-- <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/add">Add</router-link> |
      <router-link to="/delete">Delete</router-link> |
      <router-link to="/update">Update</router-link>
    </nav>
    <router-view/>
  </div> -->
  <div class="page-container">
    <md-app>
      <md-app-toolbar class="md-primary">
        <span class="md-title">Diet Log</span>
      </md-app-toolbar>

      <md-app-drawer md-permanent="full">
        <md-toolbar class="md-transparent" md-elevation="0">
          Anne Zhou
        </md-toolbar>

        <md-list>
          <md-list-item>
            <md-icon>home</md-icon>
            <span class="md-list-item-text"><router-link to="/">Home</router-link></span>
          </md-list-item>

          <md-list-item>
            <md-icon>info</md-icon>
            <span class="md-list-item-text"><router-link to="/about">About</router-link> </span>
          </md-list-item>

          <md-list-item>
            <md-icon>add</md-icon>
            <span class="md-list-item-text"><router-link to="/add">Add</router-link></span>
          </md-list-item>

          <md-list-item>
            <md-icon>delete</md-icon>
            <span class="md-list-item-text"><router-link to="/delete">Delete</router-link> </span>
          </md-list-item>

          <md-list-item>
            <md-icon>update</md-icon>
            <span class="md-list-item-text"><router-link to="/update">Update</router-link> </span>
          </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <router-view/>
        </md-app-content>
    </md-app>
  </div>
</template>

<style>
.md-app {
    border: 1px solid rgba(#000, .12);
    height: calc(100vw - 45vw);
  }

  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }
</style>
