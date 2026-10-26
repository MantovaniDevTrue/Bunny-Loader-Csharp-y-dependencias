# Dependências do Bunny Loader C#

Este repositório mantém os fontes e as dependências usadas pela revisão C# integrada de 26/10/2026. Os componentes gerenciados e nativos são versionados juntos para evitar incompatibilidades entre SDK, compilador e host.

## Runtime e compilador

| Componente | Arquivos |
| --- | --- |
| Mono ARM64 modificado | [`libmonosgen-2.0.so`](../app/src/main/jniLibs/arm64-v8a/libmonosgen-2.0.so) |
| Bibliotecas nativas do .NET | [`app/src/main/jniLibs/arm64-v8a/`](../app/src/main/jniLibs/arm64-v8a/) |
| 175 DLLs gerenciadas | [`app/src/main/assets/managed/`](../app/src/main/assets/managed/) |
| Roslyn | `Microsoft.CodeAnalysis.dll`, `Microsoft.CodeAnalysis.CSharp.dll`, `BunnySourceCompiler.dll` |
| SDK de autoria | [`BunnyCsSdk/`](../experiments/csharp/BunnyCsSdk/) e [`BunnySourceSdk/`](../experiments/csharp/BunnySourceSdk/) |
| Manifesto de integridade | [`framework.sha256`](../app/src/main/assets/managed/framework.sha256) |
| Código e patches Mono | [`tools/mono/`](../tools/mono/) |

Os projetos `BunnySourceSdk`, `BunnySourceCompiler` e `BunnyManagedProbe` têm como alvo `net8.0`. O `BunnyCsSdk` usa `net10.0` na revisão importada. O compilador declara `Microsoft.CodeAnalysis.CSharp` versão `4.11.0`. O runtime ARM64 foi preparado a partir de Mono/.NET `8.0.23` com correções documentadas em [`tools/mono/README.md`](../tools/mono/README.md).

## Ambiente Android

A configuração Gradle importa código Android/Kotlin, JNI, C++ e hooks IL2CPP. São necessários Android SDK, NDK, CMake, Gradle e Java compatíveis com a configuração do projeto. O NDK indicado em `app/build.gradle.kts` é `30.0.16248370`.

As bibliotecas do Mono fornecidas neste repositório são distintas dos binários proprietários do Terraria, como `libil2cpp.so` e `libunity.so`, que **não estão incluídos**. O host também necessita dos recursos originais do jogo para executá-lo.

## Preparação e atualização

O código atual já inclui as DLLs, as bibliotecas Mono ARM64 e os scripts para conferência. Não é preciso baixar essas mesmas dependências novamente para estudar ou reutilizar a revisão.

Para uma recompilação do Mono modificado, consulte [`tools/mono/README.md`](../tools/mono/README.md). Os scripts também explicam a ordem de preparação das DLLs e a instalação da biblioteca corrigida.

Ao atualizar Mono, Roslyn ou o SDK, revise em conjunto as dependências do compilador, os contratos do worker, as bibliotecas ARM64 e o manifesto de hashes. Evite substituir apenas um artefato isolado, pois ele pode deixar de corresponder à revisão dos demais.

## Licenças e arquivos externos

As licenças gerais e avisos de terceiros estão em [`LICENSE.md`](../LICENSE.md), [`LICENSING.md`](../LICENSING.md) e [`THIRD_PARTY_NOTICES.md`](../THIRD_PARTY_NOTICES.md). A licença do Mono acompanha o pacote em [`tools/mono/prebuilt/arm64-v8a/`](../tools/mono/prebuilt/arm64-v8a/).

Não são distribuídos APKs, chaves de assinatura, dumps, bibliotecas proprietárias do Terraria/Unity ou recursos privados do jogo.
