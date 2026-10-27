# Dependências do Bunny Loader C#

Os arquivos foram sincronizados do [commit `4119582942c4`](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/commit/4119582942c43b3dc52f4edf96c366a190630ac9). Não misture DLLs, headers, bibliotecas nativas ou fontes de versões diferentes.

## Runtime e projeto Android

| Componente | Local |
| --- | --- |
| MonoVM ARM64 e bibliotecas nativas | [`app/src/main/jniLibs/arm64-v8a/`](../app/src/main/jniLibs/arm64-v8a/) |
| Roslyn, worker, SDK e assemblies gerenciados | [`app/src/main/assets/managed/`](../app/src/main/assets/managed/) |
| Mono ARM64, ferramentas e patches | [`tools/mono/`](../tools/mono/) |
| API de mods C# | [`experiments/csharp/BunnyCsSdk/`](../experiments/csharp/BunnyCsSdk/) |
| SDK de compilação de fontes | [`experiments/csharp/BunnySourceSdk/`](../experiments/csharp/BunnySourceSdk/) |
| Compilador Roslyn | [`experiments/csharp/BunnySourceCompiler/`](../experiments/csharp/BunnySourceCompiler/) |
| Worker MonoVM | [`experiments/csharp/BunnyManagedProbe/`](../experiments/csharp/BunnyManagedProbe/) |
| Hooks C++ e ponte IL2CPP | [`app/src/main/cpp/experiments/csharp/`](../app/src/main/cpp/experiments/csharp/) |
| Serviço Kotlin Android | [`app/src/main/kotlin/dev/bunnyloader/csharp/`](../app/src/main/kotlin/dev/bunnyloader/csharp/) |

A compilação Android utiliza os arquivos Gradle e CMake do projeto. Os testes gerenciados podem ser executados separadamente a partir dos projetos `.csproj`; isso não produz um APK jogável.

## Exemplos e testes

O [ExampleMod C#](../samples/ExampleModCSharp/) acompanha a revisão integrada, junto com os testes de regressão em [`tests/`](../tests/). Os exemplos JavaScript exigidos pelo host original permanecem para preservar a compilação do Bunny Loader.

A importação também verifica a presença das bibliotecas Mono, DLLs e arquivos de integração. A QA Android de origem aprovou a compilação e a assinatura do [APK de referência](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp-Builds/releases/tag/csharp-unified-qa-4119582942c4).

## Arquivos proprietários

Este repositório não publica `libil2cpp.so`, `libunity.so`, dados ou assets proprietários do Terraria, dumps, APKs nem chaves de assinatura. Esses arquivos precisam ser fornecidos legalmente durante um build do host integrado.

A ausência dos arquivos do Terraria não significa ausência das bibliotecas do MonoVM/Roslyn. São dependências distintas.
