# Integração do suporte C#

Este repositório contém o núcleo C# do Bunny Loader integrado ao projeto Android, na revisão `v1.0` de 19/10/2026. Os arquivos nativos, gerenciados e as bibliotecas de runtime pertencem à mesma revisão.

## Componentes

| Local | Responsabilidade |
| --- | --- |
| [`BunnyCsSdk`](../experiments/csharp/BunnyCsSdk/) | API pública dos mods |
| [`BunnySourceSdk`](../experiments/csharp/BunnySourceSdk/) | Referências e contratos |
| [`BunnySourceCompiler`](../experiments/csharp/BunnySourceCompiler/) | Compilação Roslyn |
| [`BunnyManagedProbe`](../experiments/csharp/BunnyManagedProbe/) | Worker gerenciado |
| [`ManagedRuntime.cpp`](../app/src/main/cpp/experiments/csharp/ManagedRuntime.cpp) | Ponte de execução MonoVM |
| [`AutoSourceRuntime.cpp`](../app/src/main/cpp/experiments/csharp/AutoSourceRuntime.cpp) | Descoberta, preparação e carregamento das fontes |
| [`ManagedProbeService.kt`](../app/src/main/kotlin/dev/bunnyloader/csharp/ManagedProbeService.kt) | Serviço Android C# |
| [`CMakeLists.txt`](../app/src/main/cpp/CMakeLists.txt) | Integração do código nativo com o host |

## Fluxo

O host inicializa o suporte C#, descobre os mods e prepara suas fontes. O Roslyn compila as classes usando o SDK, e o MonoVM carrega o código gerenciado. As pontes JNI/C++ e IL2CPP registram conteúdo e ligam eventos aos métodos do Terraria Android.

O host continua com suas rotinas nativas e JavaScript para as demais funcionalidades do Bunny, mas não é necessário escrever callbacks C# como scripts JS.

As operações que alteram objetos do Terraria precisam respeitar o contexto de execução, os hooks e as regras de ciclo de vida definidos pela integração nativa. Os contratos de cada loader dependem da versão do jogo.

## Arquivos essenciais para compilar

A raiz conserva o Gradle e o projeto Android. Os fontes necessários incluem `app/src/main/cpp/`, `app/src/main/kotlin/`, `app/src/main/java/`, o CMake, o SDK gerenciado e os arquivos de suporte do Mono. O QuickJS do Bunny original também permanece porque faz parte do host.

As dependências C# gerenciadas já estão em `app/src/main/assets/managed/`, e as bibliotecas Mono ARM64 em `app/src/main/jniLibs/arm64-v8a/`. Não é necessário combinar esses arquivos com binários de outra branch.

Os dois exemplos originais de JavaScript mantidos em `samples/` são referenciados pelo build do Bunny. O `StarterModCSharp` serve apenas como exemplo de autoria; não é uma dependência do runtime.

## Escopo desta entrega

A base integrada anterior foi selecionada para **não carregar os loaders experimentais da linha de QA atual**. Foram removidos os projetos e exemplos recentes que não são necessários ao funcionamento do núcleo. Os fontes do host Android foram mantidos porque alguns deles são dependências diretas dos arquivos C#.

Esta seleção não altera a implementação interna de MonoVM, Roslyn, JNI, IL2CPP nem do compilador da revisão escolhida. A integridade dos arquivos foi conferida contra o commit de origem; uma build de verificação no GitHub não equivale a testar cada comportamento em um aparelho real.

Consulte [Dependências](DEPENDENCIAS.md) e [Origem da base](../SOURCE_VERSION.md).
