# Integração C# no Bunny Loader

Esta árvore mantém o projeto Android completo junto do suporte C# para que os includes, o CMake, os serviços Kotlin e o carregamento de bibliotecas permaneçam nos caminhos originais.

## Componentes

| Componente | Localização |
| --- | --- |
| API de autoria | [`experiments/csharp/BunnyCsSdk/`](../experiments/csharp/BunnyCsSdk/) |
| SDK de compilação | [`experiments/csharp/BunnySourceSdk/`](../experiments/csharp/BunnySourceSdk/) |
| Roslyn e cache | [`experiments/csharp/BunnySourceCompiler/`](../experiments/csharp/BunnySourceCompiler/) |
| Runtime gerenciado | [`experiments/csharp/BunnyManagedProbe/`](../experiments/csharp/BunnyManagedProbe/) |
| MonoVM, filas e registro nativo | [`app/src/main/cpp/experiments/csharp/`](../app/src/main/cpp/experiments/csharp/) |
| Inicialização do host | [`app/src/main/cpp/boot/`](../app/src/main/cpp/boot/) |
| Ligação JNI e serviços Android | [`app/src/main/kotlin/dev/bunnyloader/csharp/`](../app/src/main/kotlin/dev/bunnyloader/csharp/) |
| Bibliotecas C++ de conteúdo e IL2CPP | [`app/src/main/cpp/`](../app/src/main/cpp/) |

## Funcionamento

1. O Bunny Loader descobre os mods, registra suas informações e prepara o runtime C#.
2. O compilador Roslyn carrega as referências do SDK, compila as fontes dos mods e utiliza o cache quando aplicável.
3. O worker MonoVM carrega e executa as classes gerenciadas.
4. A ponte JNI/C++ comunica o runtime gerenciado com o host do Terraria Android.
5. Registradores de conteúdo, hooks, filas e callbacks conectam classes C# aos métodos e estruturas nativas do jogo.

Os módulos nativos fazem as operações de tempo crítico sem exigir que cada callback passe por JavaScript. Algumas funcionalidades visuais do host ainda compartilham infraestrutura com o Bunny original; cada loader deve ser avaliado individualmente.

## Compilação do Android

Abra a raiz do projeto no Android Studio. O build utiliza [`build.gradle.kts`](../build.gradle.kts), [`settings.gradle.kts`](../settings.gradle.kts), [`app/build.gradle.kts`](../app/build.gradle.kts) e [`app/src/main/cpp/CMakeLists.txt`](../app/src/main/cpp/CMakeLists.txt).

A configuração importada define `compileSdk 34`, `minSdk 24`, `targetSdk 34`, NDK `30.0.16248370` e suporte nativo ARM64. Instale as versões requeridas pelo próprio projeto antes de tentar o build.

As DLLs do Roslyn e do Mono e as bibliotecas ARM64 usadas nessa revisão já estão em seus caminhos de empacotamento. **Não é necessário copiar essas dependências de outro repositório.**

O host ainda depende de partes proprietárias do Terraria não distribuídas aqui. Sem as bibliotecas e os assets do jogo legalmente fornecidos pelo responsável pela build, não é possível executar o Terraria integrado. Consulte [`app/src/main/jniLibs/arm64-v8a/README.md`](../app/src/main/jniLibs/arm64-v8a/README.md).

## Desenvolvimento de mods C#

Consulte [`samples/ExampleModCSharp/`](../samples/ExampleModCSharp/) e os contratos em [`docs/csharp/`](csharp/). Os exemplos usam a API Bunny, com os fontes do ExampleModBunny como referência de comportamento.

A infraestrutura MonoVM/Roslyn é distinta da implementação completa de todos os loaders. Um novo loader pode exigir contratos e hooks nativos adicionais, sem alterações no compilador.

A revisão de origem é fixa e está registrada em [`SOURCE_VERSION.md`](../SOURCE_VERSION.md). Não misture DLLs, nativos e SDK de revisões diferentes sem atualizar o conjunto.
