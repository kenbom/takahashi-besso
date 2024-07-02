<script>
  import { createForm } from 'felte';
  // import { handleSubmit } from 'felte';
  // バリデーションスキーマの定義
  const { form, errors, validateForm } = createForm({
    initialValues: {
      name: '',
      email: '',
      inquiry: '',
    },
    validate: (values) => {
      const errors = {};
      if (!values.name) {
        errors.name = '名前を入力してください。';
      }
      if (!values.email) {
        errors.email = 'メールアドレスを入力してください。';
      } else if (!/\S+@\S+\.\S+/.test(values.email)) {
        errors.email = '有効なメールアドレスを入力してください。';
      }
      if (!values.inquiry) {
        errors.inquiry = 'お問合せ内容を入力してください。';
      }
      return errors;
    },
    onSubmit: async (values, context) => {
      // フォームの送信処理
      console.log('送信データ:', values);
      window.alert('フォームが送信されました。');
    },
  });
</script>

<form use:form>
  <label for="name">お名前</label>
  <input type="text" name="name" />
  {#if $errors.name}
    <p>
      {$errors.name[0]}
    </p>
  {/if}

  <label for="email">Eメール</label>
  <input type="text" name="email" />
  {#if $errors.email}
    <p>
      {$errors.email[0]}
    </p>
  {/if}

  <label for="inquiry">お問合せ内容</label>
  <textarea name="inquiry" class="inquiry-text" />
  {#if $errors.inquiry}
    <p>
      {$errors.inquiry[0]}
    </p>
  {/if}

  <button
    type="submit"
    class="text-gray-900 bg-gray-100 border border-gray-600 focus:outline-none hover:bg-gray-200 focus:ring-4 focus:ring-gray-100 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-600 dark:focus:ring-gray-700"
    >送信</button
  >
</form>

<style>
  form {
    display: grid;
    gap: 15px 10px;
    grid-template-columns: [labels] auto [controls] 1fr;
    @media (max-width: 496px) {
      font-size: small;
    }
  }
  form > * {
    grid-column: controls;
    font: 1em sans-serif;
  }
  form > label {
    grid-column: labels;
    justify-self: end;
    align-self: center;
    font-family: Shippori Mincho;
    @media (max-width: 496px) {
      grid-column: controls;
      justify-self: start;
      align-self: end;
      margin-bottom: -10px;
    }
  }
  form > button {
    grid-column: 1 / -1;
    font-family: Shippori Mincho;
    /* 以下と同様
  grid-column-start: 1;
  grid-column-end: -1;
  */
  }

  .inquiry-text {
    height: 400px;
  }

  p {
    margin-top: -15px;
    color: #e31313;
  }
</style>
