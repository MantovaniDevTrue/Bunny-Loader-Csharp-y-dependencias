# Bunny Loader C# — Núcleo e dependências

Código-fonte do suporte C# do [Bunny Loader](https://github.com/JonataOliveiraa/Bunny-Loader), desenvolvido para Terraria Android.

Esta árvore contém **a base C# integrada e as dependências da mesma revisão**, sem os loaders experimentais das branches mais recentes. A referência é a versão [`v1.0`](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/tree/v1.0), commit [`cfbe784e`](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/commit/cfbe784ee3cbc0ba2fabafce56c59e6eac41b67b), de 19/10/2026.

## Como funciona

O suporte é formado por quatro componentes principais:

| Parte | Função |
| --- | --- |
| **Roslyn** | Compila os arquivos `.cs` dos mods, utilizando referências do SDK. |
| **MonoVM** | Carrega e executa o código gerenciado no Android. |
| **SDK C#** | Expõe classes para conteúdo, entidades, acessórios, eventos e hooks suportados. |
| **Ponte C++ / JNI / IL2CPP** | Conecta o runtime C# aos registros e callbacks do Terraria Android. |

O host do Bunny Loader prepara o runtime e descobre os mods. O compilador processa as fontes C#, o MonoVM executa as classes gerenciadas e a integração nativa conecta os eventos ao jogo. A execução dos callbacks C# não exige traduzi-los para JavaScript.

Os módulos originais do Bunny Loader que fazem parte do processo de inicialização e compilação Android foram preservados, inclusive o QuickJS utilizado pelo host. Eles não representam uma segunda implementação do C#.

## Organização dos arquivos

| Local | Conteúdo |
| --- | --- |
| [`experiments/csharp/BunnyCsSdk/`](experiments/csharp/BunnyCsSdk/) | API de autoria C# |
| [`experiments/csharp/BunnySourceSdk/`](experiments/csharp/BunnySourceSdk/) | Referências para compilar mods C# |
| [`experiments/csharp/BunnySourceCompiler/`](experiments/csharp/BunnySourceCompiler/) | Roslyn, análise e cache |
| [`experiments/csharp/BunnyManagedProbe/`](experiments/csharp/BunnyManagedProbe/) | Worker gerenciado |
| [`experiments/csharp/BunnyCsPackager/`](experiments/csharp/BunnyCsPackager/) | Ferramentas de empacotamento |
| [`app/src/main/cpp/experiments/csharp/`](app/src/main/cpp/experiments/csharp/) | MonoVM, hooks e integração nativa |
| [`app/src/main/kotlin/dev/bunnyloader/csharp/`](app/src/main/kotlin/dev/bunnyloader/csharp/) | Serviço Android C# |
| [`app/`](app/) | Host Android e infraestrutura necessária para compilar e executar |
| [`tools/mono/`](tools/mono/) | Fonte, patch e ferramentas do Mono ARM64 |
| [`tests/`](tests/) | Testes da base e componentes nativos |

Os dois exemplos JavaScript do Bunny original foram conservados porque são referenciados pelo build do host. O [StarterMod C#](samples/StarterModCSharp/) permanece como exemplo pequeno. Os exemplos C# experimentais e os loaders recentes não fazem parte desta entrega.

## Dependências fornecidas

- **Mono ARM64 corrigido:** [`app/src/main/jniLibs/arm64-v8a/`](app/src/main/jniLibs/arm64-v8a/), acompanhado dos demais componentes nativos do .NET.
- **DLLs do runtime, compilador e SDK:** [`app/src/main/assets/managed/`](app/src/main/assets/managed/).
- **Fontes e recompilação do Mono:** [`tools/mono/`](tools/mono/).
- **Projeto de compilação Android:** [`build.gradle.kts`](build.gradle.kts), [`app/build.gradle.kts`](app/build.gradle.kts) e [`CMakeLists.txt`](app/src/main/cpp/CMakeLists.txt).

As bibliotecas, DLLs, fontes e contratos nativos foram retirados **da mesma revisão**, evitando misturar implementações recentes com dependências antigas.

## Compilação e limites

A raiz contém o projeto Android, que pode ser aberto no Android Studio com as ferramentas exigidas pelas configurações Gradle e CMake. O runtime nativo dessa entrega é ARM64. Os projetos C# podem ser inspecionados e compilados separadamente por meio dos arquivos `.csproj`.

**Este repositório não distribui o Terraria nem é um APK jogável pronto.** Os binários e assets proprietários do jogo e as chaves de assinatura permanecem fora do GitHub. A execução do Terraria integrado depende desses componentes obtidos legalmente.

O núcleo MonoVM/Roslyn foi exercitado durante o desenvolvimento anterior. Esta seleção foi conferida quanto à integridade dos arquivos, mas **não foi submetida a uma nova sessão de gameplay no aparelho** depois da extração. Isso é diferente de afirmar que todos os loaders estão concluídos.

Para detalhes, consulte [Integração C#](docs/INTEGRACAO.md), [Dependências](docs/DEPENDENCIAS.md) e [Revisão de origem](SOURCE_VERSION.md).

## Créditos

**Bunny Loader original:** Jonata Oliveira.  
**Integração C#:** Mantovani.

Os avisos de licença e de terceiros foram preservados junto aos fontes.
