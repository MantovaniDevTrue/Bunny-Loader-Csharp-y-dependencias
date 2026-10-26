# Dependências do núcleo C#

As dependências desta entrega foram extraídas da mesma revisão integrada do Bunny Loader C# (`v1.0`, commit `cfbe784ee3cbc0ba2fabafce56c59e6eac41b67b`).

## Runtime e SDK

| Componente | Localização |
| --- | --- |
| MonoVM ARM64 modificado | [`app/src/main/jniLibs/arm64-v8a/`](../app/src/main/jniLibs/arm64-v8a/) |
| DLLs do framework, Roslyn e SDK | [`app/src/main/assets/managed/`](../app/src/main/assets/managed/) |
| Código e scripts do Mono | [`tools/mono/`](../tools/mono/) |
| SDK C# | [`experiments/csharp/BunnyCsSdk/`](../experiments/csharp/BunnyCsSdk/) |
| Referências dos mods-fonte | [`experiments/csharp/BunnySourceSdk/`](../experiments/csharp/BunnySourceSdk/) |
| Compilador Roslyn | [`experiments/csharp/BunnySourceCompiler/`](../experiments/csharp/BunnySourceCompiler/) |
| Worker | [`experiments/csharp/BunnyManagedProbe/`](../experiments/csharp/BunnyManagedProbe/) |

As DLLs e as bibliotecas nativas estão presentes nos diretórios utilizados pelo Gradle. A biblioteca Mono modificada possui documentação, licença e hashes em [`tools/mono/`](../tools/mono/).

## Ambiente de compilação

O projeto Android utiliza Gradle, Kotlin, CMake e NDK, com as versões exigidas pelos arquivos [`build.gradle.kts`](../build.gradle.kts) e [`app/build.gradle.kts`](../app/build.gradle.kts). A integração nativa é destinada ao Android ARM64.

Os projetos C# podem ser inspecionados por meio dos arquivos `.csproj`; sua compilação separada não gera um APK Android.

O código original do host Bunny foi mantido, inclusive JNI, hooks IL2CPP, inicialização e recursos necessários ao funcionamento do aplicativo. Remover módulos desse host sem revisar o CMake e o Gradle pode deixar a integração C# incompleta.

## Componentes não incluídos

Este repositório **não distribui** `libil2cpp.so`, `libunity.so`, assets proprietários do Terraria/Unity, dumps do jogo, APKs nem chaves de assinatura. O responsável pela compilação precisa fornecer legalmente esses componentes fora do repositório.

A ausência dos binários do Terraria não indica falta de alguma biblioteca do MonoVM ou do Roslyn. São dependências diferentes.

## Atualizações

Não substitua apenas as DLLs ou o Mono por arquivos de branches recentes. Ao atualizar o suporte C#, os contratos do SDK, o compilador, a JNI, os hooks nativos e as bibliotecas devem acompanhar a mesma revisão.

Consulte [Integração](INTEGRACAO.md) e [Versão de origem](../SOURCE_VERSION.md).
