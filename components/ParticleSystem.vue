<template>
  <div>
    <no-ssr>
      <template>
        <Scene style="position: fixed; z-index: 5; height: 40rem;">
          <Property
            name="clearColor"
            auto-clear="false"
          />
          <HemisphericLight
            diffuse="#08F7C9"
            specular="#0FAFF9'"
          />
          <Camera :position="[100, 50, -70]" />
          <Entity :position="[0, 0, 20]">
            <Sphere :position="[100, 80, 0]">
              <Animation
                property="position.x"
                :duration="90"
                :end="Math.PI * 70"
              />
            </Sphere>
            <Sphere :position="[100, 40, 0]">
              <Animation
                property="position.x"
                :duration="20"
                :end="Math.PI * 70"
              />
            </Sphere>
            <Sphere :position="[0, 0, 0]">
              <Animation
                property="position.x"
                :duration="30"
                :end="Math.PI * 70"
              />
              <Animation
                property="position.y"
                :duration="60"
                :end="Math.PI * 70"
              />
            </Sphere>
            <Sphere :position="[50, 0, 50]">
              <Animation
                property="position.x"
                :duration="50"
                :end="Math.PI * 70"
              />
              <Animation
                property="position.y"
                :duration="60"
                :end="Math.PI * 70"
              />
            </Sphere>
          </Entity>
        </Scene>
      </template>
    </no-ssr>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myScene: null,
      myEntity: null,
      myBox: null,
    };
  },
  watch: {
    myScene() {
      // myEntity is now available from the component
      // do something with it here or call a method to use it from here

    },
    myEntity() {
      // myEntity is now available from the component
      // do something with it here or call a method to use it from here

    },

    myBox() {
      // myBox is now available from the component
      // do something with it here or call a method to use it from here
    },
  },
}
</script>

<style scoped>
</style>
