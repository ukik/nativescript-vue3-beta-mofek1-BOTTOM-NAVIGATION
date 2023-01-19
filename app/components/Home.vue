<script lang="ts" setup>
import {
  ref,
  computed,
  onMounted,
  onUnmounted,
  $navigateTo,
  toRaw,
} from 'nativescript-vue';
import { View } from '@nativescript/core';
import Details from './Details.vue';

const indexSelected = ref(0);
const refFirstLabel = ref();
const refSecondLabel = ref();
const refThirdLabel = ref();
const classSelected = 'bg-green-500 rounded-full px-4 py-2';

function selectView(args, index) {
  indexSelected.value = index;
  const labelFirstView: View = toRaw(refFirstLabel.value.nativeView);
  const labelSecondView: View = toRaw(refSecondLabel.value.nativeView);
  const labelThirdView: View = toRaw(refThirdLabel.value.nativeView);
  const views = [labelFirstView, labelSecondView, labelThirdView];
  views.forEach((view, currentIndex) => {
    if (currentIndex == index) {
      view.animate({
        width: 'auto',
        duration: 250,
      });
    } else {
      view.animate({
        width: 0,
        duration: 250,
      });
    }
  });
}
onMounted(() => {
  setTimeout(() => {
    selectView(null, 0);
  }, 200);
});
</script>

<template>
  <Frame>
    <Page>
      <ActionBar>
        <Label text="Home" class="font-bold text-lg" />
      </ActionBar>

      <GridLayout rows="*, 75">
        <Label
          row="0"
          class="text-xl align-middle text-center text-gray-500"
          text="EXAMPLE"
        />

        <FlexboxLayout
          row="1"
          columns="*,*,*"
          class="bg-green-400 justify-around items-center"
        >
          <FlexboxLayout
            @tap="selectView($event, 0)"
            class="justify-center items-center"
            :class="[indexSelected === 0 ? classSelected : '']"
          >
            <Image
              height="32"
              src="https://cdn-icons-png.flaticon.com/512/456/456212.png"
            />
            <Label ref="refFirstLabel" width="0" text="asdff" />
          </FlexboxLayout>

          <FlexboxLayout
            @tap="selectView($event, 1)"
            class="justify-center items-center"
            :class="[indexSelected === 1 ? classSelected : '']"
          >
            <Image
              height="32"
              src="https://cdn-icons-png.flaticon.com/512/456/456212.png"
            />
            <Label ref="refSecondLabel" width="0" text="asdfx" />
          </FlexboxLayout>

          <FlexboxLayout
            @tap="selectView($event, 2)"
            class="justify-center items-center"
            :class="[indexSelected === 2 ? classSelected : '']"
          >
            <Image
              height="32"
              src="https://cdn-icons-png.flaticon.com/512/456/456212.png"
            />
            <Label ref="refThirdLabel" width="0" text="asdfa" />
          </FlexboxLayout>
        </FlexboxLayout>
      </GridLayout>
    </Page>
  </Frame>
</template>

<style>
/* .info {
    font-size: 20;
  } */
</style>
