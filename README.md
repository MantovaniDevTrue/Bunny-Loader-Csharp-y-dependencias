# Bunny Loader C# — Código-fonte e dependências

Suporte C# integrado ao [Bunny Loader](https://github.com/JonataOliveiraa/Bunny-Loader), desenvolvido para Terraria Mobile. Este repositório contém **o projeto Android, o núcleo C# e as dependências usadas na mesma revisão**, com os arquivos nos caminhos originais de compilação.

A execução dos mods C# utiliza **Roslyn + MonoVM**, com a integração nativa em C++/IL2CPP. O suporte JavaScript do Bunny Loader permanece no host original, mas os callbacks gerenciados usam o runtime C#.

## Arquitetura

| Componente | Função |
| --- | --- |
| **Roslyn** | Compila os arquivos `.cs` dos mods e utiliza as referências do SDK. |
| **MonoVM** | Carrega e executa o código gerenciado por meio do worker Android. |
| **SDK C#** | Fornece as classes e contratos de autoria, incluindo itens, projéteis, NPCs, equipamentos, hooks e eventos. |
| **C++ / IL2CPP** | Registra conteúdo, integra hooks e executa operações nativas no Terraria Android. |
| **JNI / Kotlin** | Faz a comunicação com o serviço Android e com o runtime gerenciado. |

O fluxo básico é: descoberta do mod → compilação/carga das classes C# → registro do conteúdo → callbacks e eventos ligados aos métodos do jogo.

O MonoVM e o Roslyn já foram utilizados nas builds de desenvolvimento. **Os loaders e suas APIs específicas continuam em evolução**; isso não implica reconstruir o compilador ou o runtime.

## Estrutura do repositório

| Diretório | Conteúdo |
| --- | --- |
| [`app/`](app/) | Projeto Android completo, C++/IL2CPP, JNI, Kotlin/Java, recursos e bibliotecas necessárias |
| [`experiments/csharp/`](experiments/csharp/) | SDK C#, Roslyn, MonoVM, assemblies e projetos gerenciados |
| [`samples/`](samples/) | ExampleMod C# e outros exemplos em C# |
| [`tests/`](tests/) | Testes de runtime, hooks, compilação, conteúdo e integração |
| [`tools/`](tools/) | Scripts de build, Mono ARM64, geração e preparação das dependências |
| [`docs/csharp/`](docs/csharp/) | Contratos, documentação e referências técnicas |

Os arquivos mais importantes são:

- [`BunnySourceCompiler/`](experiments/csharp/BunnySourceCompiler/) — compilação Roslyn.
- [`BunnySourceSdk/`](experiments/csharp/BunnySourceSdk/) e [`BunnyCsSdk/`](experiments/csharp/BunnyCsSdk/) — APIs e referências de compilação.
- [`BunnyManagedProbe/`](experiments/csharp/BunnyManagedProbe/) — componentes gerenciados do worker.
- [`ManagedRuntime.cpp`](app/src/main/cpp/experiments/csharp/ManagedRuntime.cpp) — execução e comunicação nativa.
- [`AutoSourceRuntime.cpp`](app/src/main/cpp/experiments/csharp/AutoSourceRuntime.cpp) — carregamento de mods-fonte.
- [`ManagedProbeService.kt`](app/src/main/kotlin/dev/bunnyloader/csharp/ManagedProbeService.kt) — serviço Android.
- [`ExampleModCSharp/`](samples/ExampleModCSharp/) — fontes e assets de exemplo.

## Dependências incluídas

Este repositório preserva as dependências necessárias à integração conforme a revisão de origem:

- **DLLs gerenciadas:** [`app/src/main/assets/managed/`](app/src/main/assets/managed/), incluindo framework Mono/.NET, Roslyn, compilador e SDK.
- **Bibliotecas ARM64:** [`app/src/main/jniLibs/arm64-v8a/`](app/src/main/jniLibs/arm64-v8a/), incluindo o Mono modificado.
- **Fonte e patch do Mono:** [`tools/mono/`](tools/mono/), com licença, SHA-256 e scripts de recompilação.
- **Configuração nativa:** [`CMakeLists.txt`](app/src/main/cpp/CMakeLists.txt) e [`app/build.gradle.kts`](app/build.gradle.kts).
- **Engine de suporte do Bunny:** mantida na árvore Android para que as dependências entre módulos não sejam quebradas.

Não é necessário reconstruir manualmente o Mono ou o Roslyn apenas para consultar e integrar esta revisão: os artefatos gerenciados e ARM64 usados pelo projeto estão nos diretórios correspondentes.

## Compilação

O projeto é destinado ao Android ARM64. Para compilar o aplicativo, é necessário um ambiente Android Studio/Gradle com SDK, NDK e CMake compatíveis com as versões declaradas no projeto. O Gradle usa as bibliotecas e os assemblies incluídos na árvore.

Para inspecionar ou compilar apenas os projetos C#, use os arquivos `.csproj` em `experiments/csharp/` com o SDK .NET adequado. Essa compilação **não equivale a gerar um APK**.

Consulte [`docs/INTEGRACAO.md`](docs/INTEGRACAO.md) para o fluxo Android e [`docs/DEPENDENCIAS.md`](docs/DEPENDENCIAS.md) para os detalhes dos componentes.

## Versão e origem

Esta importação utiliza o commit fixo [`e03e7d8d2940`](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/commit/e03e7d8d29405ac23c7b084471d40089f97a1ab9), de 26/10/2026, do projeto [Bunnyloader-Csharp](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp). O snapshot foi mantido fixo para que os arquivos do SDK, do runtime e das dependências sejam compatíveis entre si.

A origem e a seleção de arquivos estão registradas em [`SOURCE_VERSION.md`](SOURCE_VERSION.md). Novas alterações no repositório de desenvolvimento não entram automaticamente aqui.

## Créditos

**Bunny Loader original:** Jonata Oliveira.  
**Integração C#:** Mantovani.

As licenças e os avisos de terceiros foram preservados. Não são distribuídos binários ou recursos proprietários do Terraria/Unity, dumps do jogo, APKs ou chaves de assinatura.
