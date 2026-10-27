# Integração C# no Bunny Loader

Esta versão corresponde ao commit [`4119582942c4`](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/commit/4119582942c43b3dc52f4edf96c366a190630ac9), utilizado no APK 1.0.25 validado no Terraria Android.

## Fluxo de execução

1. O host Android identifica os mods C# e prepara as fontes.
2. O Roslyn compila os arquivos `.cs` com as referências do `BunnySourceSdk`.
3. O MonoVM carrega os assemblies e executa as classes gerenciadas.
4. As pontes JNI/C++ e IL2CPP registram o conteúdo e chamam os métodos do Terraria Android.

Os callbacks escritos em C# não são convertidos em JavaScript. O JavaScript que permanece na árvore pertence ao host Bunny Loader e aos exemplos originais de seu build.

## Organização

- **SDK e compilador:** `experiments/csharp/BunnyCsSdk/`, `BunnySourceSdk/` e `BunnySourceCompiler/`.
- **Execução gerenciada:** `BunnyManagedProbe/` e `app/src/main/cpp/experiments/csharp/ManagedRuntime.cpp`.
- **Carregamento:** `app/src/main/cpp/experiments/csharp/AutoSourceRuntime.cpp`.
- **Ponte Android:** `app/src/main/kotlin/dev/bunnyloader/csharp/ManagedProbeService.kt`.
- **Bibliotecas:** `app/src/main/assets/managed/`, `app/src/main/jniLibs/arm64-v8a/` e `tools/mono/`.
- **Exemplo C#:** `samples/ExampleModCSharp/`.

## Classes de dano

A revisão integra `DamageClassLoader` e os hooks nativos de combate. Os cálculos consideram a classe de dano do item para dano, crítico, knockback e velocidade de uso. Também existe atualização das linhas de tooltip relacionadas aos atributos.

No Android, a obtenção do jogador local utiliza `Main.get_LocalPlayer`, evitando tratar `Main.myPlayer` como campo. Os logs de diagnóstico informam quando referências nativas necessárias não são encontradas e distinguem valores originais e valores finais aplicados.

## Validação

A [QA da revisão](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp/actions/runs/40434694323) aprovou contratos, compilação Android e empacotamento assinado. O APK foi testado no Terraria Android com resultado positivo. A sincronização deste repositório também executa testes gerenciados e nativos de `DamageClass`.

A base conserva as interfaces de pesquisa e outras rotas da revisão original onde forem necessárias às dependências do host. O teste em aparelho confirma a build validada; APIs e exemplos não exercitados individualmente não devem ser anunciados como plenamente testados.

Consulte [Dependências](DEPENDENCIAS.md) e [Origem](../SOURCE_VERSION.md).
