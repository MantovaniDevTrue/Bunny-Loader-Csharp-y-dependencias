# Bunny Loader C# — código-fonte e dependências

Integração C# do [Bunny Loader](https://github.com/JonataOliveiraa/Bunny-Loader) para Terraria Android.

Este repositório reúne o projeto Android, o runtime MonoVM, o compilador Roslyn, o SDK C#, as pontes JNI/IL2CPP, exemplos, testes e dependências necessárias ao suporte C#. O motor de mods JavaScript original permanece preservado no host, mas a execução dos callbacks C# usa a infraestrutura nativa e gerenciada.

## Organização

| Pasta | Conteúdo |
| --- | --- |
| `app/` | Projeto Android, código C++/JNI/IL2CPP, Kotlin/Java, bibliotecas ARM64 e DLLs gerenciadas |
| `experiments/csharp/` | SDK C#, Roslyn, MonoVM e projetos gerenciados |
| `samples/` | Exemplos de mods C# e assets correspondentes |
| `tests/` | Testes relacionados a runtime, integração e loaders |
| `tools/` | Build do Mono, montagem das DLLs e ferramentas de suporte |
| `docs/csharp/` | Referências e contratos técnicos C# |

A base MonoVM/Roslyn está implementada. As APIs e os loaders específicos de conteúdo do Terraria continuam evoluindo. Este projeto não incorpora o runtime do tModLoader.

## Fontes e versões

A importação é baseada em um commit fixo do projeto [MantovaniDevTrue/Bunnyloader-Csharp](https://github.com/MantovaniDevTrue/Bunnyloader-Csharp), para manter código, bibliotecas e contratos da mesma revisão. O commit de origem será registrado no arquivo `SOURCE_VERSION.md`.

O aplicativo depende dos recursos do Terraria adquiridos e instalados legalmente. Binários, dumps e assets proprietários do jogo, credenciais e chaves de assinatura não são redistribuídos neste repositório.

## Créditos

Bunny Loader original: **Jonata Oliveira**. Integração C#: **Mantovani**. Licenças e avisos de terceiros mantidos na origem.
