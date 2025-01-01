<template>
  <div
    class="flex flex-col md:flex-row min-h-32 min-w-screen flex-wrap justify-center justify-items-center"
  >
    <Card class="sm:w-1/2 m-3">
      <CardHeader>
        <CardTitle>ข้อมูลผู้สูงอายุ</CardTitle>
        <CardDescription
          >วิเคราะห์โอกาสในการหกล้มของผู้สูงอายุ in one-click.</CardDescription
        >
      </CardHeader>
      <CardContent>
        <form>
          <div class="grid items-center w-full gap-4">
            <div class="flex flex-col space-y-1.5">
              <Label for="tp1">ช่วงเวลาครั้งที่ 1</Label>
              <Input
                type="number"
                id="tp1"
                placeholder="กรอกเวลา หน่วย (วินาที)"
                v-model="timePeriod1"
              />
            </div>
            <div class="flex flex-col space-y-1.5">
              <Label for="tp2">ช่วงเวลาครั้งที่ 2</Label>
              <Input
                type="number"
                id="tp2"
                placeholder="กรอกเวลา หน่วย (วินาที)"
                v-model="timePeriod2"
              />
            </div>
          </div>
        </form>
      </CardContent>
      <CardFooter class="flex justify-between px-6 pb-6">
        <Button variant="outline" @click="clear"> เคลียร์ค่า </Button>
        <Button
          class="bg-raspberryBlush hover:bg-raspberryBlush"
          @click="analyze"
          >วิเคราะห์</Button
        >
      </CardFooter>
    </Card>
    <Card class="sm:w-1/2 m-3">
      <CardHeader>
        <CardTitle>ผลลัพธ์โอกาสในการหกล้มของผู้สูงอายุ</CardTitle>
        <CardDescription
          >วิเคราะห์โอกาสในการหกล้มของผู้สูงอายุ in one-click.</CardDescription
        >
      </CardHeader>
      <CardContent>
        <div
          class="flex shrink-0 items-center justify-center justify-items-center"
        >
          <img class="h-36 w-auto rounded-full" :src="targetImage" alt="" />
        </div>
      </CardContent>
    </Card>
  </div>
</template>
<script setup lang="ts">
import { Button } from '@/components/ui/button';
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from '@/components/ui/card';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { ref, type Ref } from 'vue';

const timePeriod1: Ref<number> = ref(0);
const timePeriod2: Ref<number> = ref(0);
const targetImage: Ref<string> = ref('/thinking-cat.gif');

function clear(): void {
  timePeriod1.value = 0;
  timePeriod2.value = 0;
  resetResultImage();
}

function analyze(): void {
  if (timePeriod1.value < 0) {
    timePeriod1.value = convertToPositiveNumber(timePeriod1.value);
  }
  if (timePeriod2.value < 0) {
    timePeriod2.value = convertToPositiveNumber(timePeriod2.value);
  }
  const result: number = (timePeriod1.value + timePeriod2.value) / 2;
  const threshold: number = 12;
  if (targetImage.value != 'thinking-cat.gif') {
    resetResultImage();
  }
  setTimeout(() => {
    targetImage.value = result >= threshold ? 'high-risk.png' : 'low-risk.png';
  }, 1000);
}
function resetResultImage(): void {
    targetImage.value = 'thinking-cat.gif';
}
function convertToPositiveNumber(negativeNumber: number): number {
  return negativeNumber * -1;
}
</script>
