# Bunny Loader C# — Núcleo e dependências

Código-fonte do suporte C# do [Bunny Loader](https://github.com/JonataOliveiraa/Bunny-Loader) para Terraria Android. Esta árvore reúne o runtime, o SDK, a integração Android e as dependências da mesma revisão.

## Versão validada

- **Fonte:** [Bunnyloader-Csharp, commit `4119582942c4`](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/commit/4119582942c43b3dc52f4edf96c366a190630ac9).
- **APK de referência:** [Bunny Loader C# 1.0.25 — QA ARM64](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp-Builds/releases/tag/csharp-unified-qa-4119582942c4).
- **ExampleMod C#:** 0.1.71.
- **Validação:** compilação Android, testes automatizados e assinatura aprovados no [workflow de QA](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/actions/runs/40434694323). O APK correspondente também foi testado com sucesso no Terraria Android em aparelho real.

A sincronização mantém os arquivos nativos, gerenciados e as bibliotecas da **mesma revisão**. Não utiliza o código de alterações posteriores que ainda não fizeram parte do teste aprovado.

## Componentes

| Diretório | Função |
| --- | --- |
| [`experiments/csharp/BunnyCsSdk/`](experiments/csharp/BunnyCsSdk/) | API de desenvolvimento de mods C# |
| [`experiments/csharp/BunnySourceSdk/`](experiments/csharp/BunnySourceSdk/) | Referências e contratos do SDK |
| [`experiments/csharp/BunnySourceCompiler/`](experiments/csharp/BunnySourceCompiler/) | Compilação Roslyn |
| [`experiments/csharp/BunnyManagedProbe/`](experiments/csharp/BunnyManagedProbe/) | Worker e execução gerenciada |
| [`experiments/csharp/BunnyCsPackager/`](experiments/csharp/BunnyCsPackager/) | Empacotamento dos mods |
| [`app/src/main/cpp/experiments/csharp/`](app/src/main/cpp/experiments/csharp/) | MonoVM, hooks e integração IL2CPP |
| [`app/src/main/kotlin/dev/bunnyloader/csharp/`](app/src/main/kotlin/dev/bunnyloader/csharp/) | Serviço C# Android |
| [`app/src/main/assets/managed/`](app/src/main/assets/managed/) | DLLs e bibliotecas gerenciadas |
| [`app/src/main/jniLibs/arm64-v8a/`](app/src/main/jniLibs/arm64-v8a/) | Bibliotecas nativas ARM64 |
| [`tools/mono/`](tools/mono/) | Fontes, ferramentas e arquivos do Mono |
| [`samples/ExampleModCSharp/`](samples/ExampleModCSharp/) | Exemplo C# correspondente à versão validada |
| [`tests/`](tests/) | Contratos e testes de regressão |

A integração inclui a implementação de **DamageClass**, com cálculo de dano e crítico, knockback, velocidade de uso e atualização de tooltips. A correção Android obtém o jogador local por `Main.get_LocalPlayer` e registra referências ausentes para facilitar diagnósticos.

O host do Bunny Loader conserva os componentes JavaScript necessários às demais funcionalidades do próprio aplicativo. **Os mods C# são compilados e executados por Roslyn/MonoVM, sem precisar traduzir seus callbacks para JavaScript.** Os exemplos JavaScript originais do host permanecem no projeto.

## Compilação

O projeto Android utiliza Gradle, Kotlin, CMake e NDK. Os componentes públicos necessários ao runtime C# estão presentes, mas **não são distribuídos os binários ou assets proprietários do Terraria, chaves de assinatura nem um APK do jogo**.

Para avaliar os exemplos e os contratos, consulte [Integração](docs/INTEGRACAO.md), [Dependências](docs/DEPENDENCIAS.md) e [Revisão de origem](SOURCE_VERSION.md).

A aprovação da build no celular não é uma certificação individual de todos os loaders ou de todos os comportamentos possíveis.

## Créditos

**Bunny Loader original:** Jonata Oliveira.  
**Integração C#:** Mantovani.

Os avisos de licenciamento e as atribuições de terceiros permanecem preservados.
