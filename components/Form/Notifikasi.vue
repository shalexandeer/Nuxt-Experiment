<template>
  <div>
    <h1>Notification Setting</h1>
    <Form
      :validation-schema="validationSchema"
      @submit="onSubmit">
      <Field
        name="email"
        type="email" />
      <ErrorMessage name="email" />
      <Field
        name="password"
        type="password" />
      <ErrorMessage name="password" />
      <button>Submit</button>
    </Form>
  </div>
</template>

<script setup>
import { Form, Field, ErrorMessage } from "vee-validate";
import { toTypedSchema } from "@vee-validate/zod";
import * as zod from "zod";

const validationSchema = toTypedSchema(
  zod.object({
    email: zod
      .string()
      .min(1, { message: "This is required" })
      .email({ message: "Must be a valid email" }),
    password: zod
      .string()
      .min(1, { message: "This is required" })
      .min(8, { message: "Too short" }),
  })
);
function onSubmit(values) {
  alert(JSON.stringify(values, null, 2));
}
</script>
