---
title: Contexto Settings
description: O objeto de configurações é um proxy na parte da loja de framework do seu contexto que você pode usar para configurar seu aplicativo com informações públicas
---

O objeto `settings` é um proxy na parte da loja de framework do seu contexto que você pode usar para configurar seu aplicativo com informações públicas.

Essa chave é readwrite no contexto do server.

Essa chave é readonly no contexto do client.

As chaves de configurações serão congeladas após a [inicialização do aplicativo](/pt-br/inicializacao-da-aplicacao).

As chaves a seguir estão disponíveis no objeto:

- development: object
- production: object
- [anySetting]: any

Você pode declarar as chaves para development ou para production para ter diferentes configurações por [ambiente](/pt-br/contexto-environment). 

Se você declarar uma chave diretamente para o objeto de configurações ficará disponível em ambos os ambientes.

Quando lendo de uma chave você deve ler diretamente do objeto de configurações e Nullstack irá retornar o valor mais adequado para aquele [ambiente](/pt-br/contexto-environment).

```jsx
import Nullstack from 'nullstack';

class Application extends Nullstack {

  static async start({settings}) {
    settings.development.publicKey = 'SANDBOX_API_KEY';
    settings.production.publicKey = 'PRODUCTION_API_KEY';
    settings.endpoint = 'https://domain.com/api';
  }

  async hydrate({settings}) {
    const response = await fetch(settings.endpoint, {
      headers: {
        Authorization: `Bearer ${settings.publicKey}`
      }
    });
    this.data = await response.json();
  }

}

export default Application;
```


Qualquer chave de ambiente começando com NULLSTACK_SETTINGS_ será mapeado para as confirgurações daquele ambiente.

> 🐱‍💻 NULLSTACK_SETTINGS_PUBLIC_KEY será mapeado para settings.publicKey

## Próximo passo

⚔ Aprenda sobre [segredos de contexto](/pt-br/contexto-secrets).
