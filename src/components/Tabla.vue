<template>
    <tr class="bg-white border-b">
      <td class="py-4 px-6">{{ usuarios.nombre }}</td>
      <td class="py-4 px-6">{{ usuarios.email }}</td>
      <td class="py-4 px-6">{{ usuarios.telefono }}</td>
      <td class="py-4 px-6">{{ usuarios.genero }}</td>
    </tr>
</template>

<script>
export default {
  name: "TablaComponente",

  data() {
    return {};
  },

  props: {
    usuarios: Object,
  },
};
</script>
