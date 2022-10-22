<script setup>
    import { Inertia } from '@inertiajs/inertia';
    defineProps({
        id:String,
        blog:Object
    })


    const handleDelete = id => {
        Inertia.delete(`/inertia/${id}`, {
            onBefore: () => confirm('Are you sure you want to delete this user?'),
        })
    }
</script>

<template>
  {{id}}
  <div>件名:{{blog.title}}</div>
  <div>内容:{{blog.content}}</div>
  <button @click="handleDelete(blog.id)">削除する</button>
</template>

<style>

</style>
