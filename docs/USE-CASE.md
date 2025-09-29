# CASOS DE USO

## Caso de Uso 1 - Realizar cadastro de usuário
* **Ator:** Visitante (usuário não autenticado).
* **Resumo:** O visitante se cadastra na plataforma para se tornar um usuário, podendo criar e interagir com receitas.  
* **Pré-condições**: O visitante não pode ter uma conta existente com o e-mail fornecido.  
* **Pós-condição:** Uma nova conta de usuário é criada e está autenticada no sistema.  
* **Fluxo Principal:**  
    1. **Ator:** inicia caso de uso clicando no botão "Cadastrar".  
    2. **Sistema:** exibe um formulário de cadastro solicitando nome, e-mail e senha.  
    3. **Ator:** preenche os dados e clica em "Criar conta".  
    4. **Sistema:** valida os dados.  
        - Se o e-mail já estiver em uso, o sistema aciona o **FE1.**
        - Se os dados forem inválidos, o sistema aciona o **FE2.**
    5. **Sistema:** cria nova conta de usuário no banco de dados.  
    6. **Sistema:** autentica o novo usuário e o redireciona para a página principal.  
* **Fluxos de Exceção:**  
    - **FE1.** E-mail fornecido já está em uso:  
        1. **Sistema:** exibe a mensagem de erro: "Este e-mail já está cadastrado. Tente fazer o login."  
    - **FE2.** Os dados fornecidos são inválidos:
        1. **Sistema:** exibe uma mensagem de erro específica abaixo do campo inválido e não prossegue com o cadastro.
## Caso de uso 2 - Realizar login 
* **Ator:** Visitante.
* **Resumo:** Usuário já cadastrado acessa sua conta para utilizar as funcionalidades do sistema.  
* **Pré-condição:** **Ator:** deve possuir uma conta ativa.  
* **Pós-condição:** usuário está autenticado e com acesso às funcionalidades restritas da sua conta.  
* **Fluxo Principal:**
    1. **Ator:** inicia caso de uso clicando no botão “Login”.  
    2. **Sistema:** exibe um formulário solicitando E-mail e Senha. 
    3. **Ator:** preenche suas credenciais e clica em "Entrar". 
    4. **Sistema:** verifica se as credenciais correspondem a um usuário cadastrado.
        - Se a senha e/ou o e-mail estiverem incorretos, o sistema aciona **FE1.**  
    5. **Sistema:** autentica **Ator:** e o redireciona para a página principal.  
* **Fluxos de Exceção:**
    * **FE1.** E-mail e/ou senha incorretos: 
        1. **Sistema:** exibe a mensagem de erro: "E-mail ou senha inválidos."  

## Caso de uso 3 - Criar receita
* **Ator:** Usuário. 
* **Resumo:** Usuário cria receita, preenchendo todas as informações necessárias como título, ingredientes, modo de preparo e tags. 
* **Pré-condição:** usuário deve estar logado no sistema. 
* **Pós-condição:** uma nova receita foi criada e salva como "rascunho".
* **Fluxo Principal:** 
    1. **Ator:** inicia o caso de uso clicando no botão "Criar Nova Receita". 
    2. **Sistema:** exibe o formulário de criação de receita com os seguintes campos: Título, Descrição, Lista de Ingredientes, Modo de Preparo, Tempo de Preparo, Rendimento e um campo de busca para Tags.  
    3. **Ator:** preenche todas as informações da sua receita. 
    4. **Ator:** começa a digitar o nome de uma tag no campo **Tags** (ex: 
    “japon...”). 
    5. **Sistema:** realiza uma busca em tempo real na lista de tags existentes e exibe sugestões que correspondem ao texto digitado (ex: "Culinária Japonesa").
        - Se não existir nenhuma tag correspondente ao texto digitado, o usuário pode iniciar o **FA1.** 
    6. **Ator:** seleciona uma ou mais tags da lista de sugestões. As tags 
    selecionadas são adicionadas visualmente à receita. 
    7. **Ator:** pode adicionar uma ou mais fotos da receita. 
    8. **Ator:** clica no botão "Salvar Rascunho". 
    9. **Sistema:** valida se os campos obrigatórios (como Título, Ingredientes e Modo de Preparo) foram preenchidos.
        - Se algum campo obrigatório não for preenchido, o sistema aciona o **FE1.** 
    10. **Sistema:** salva a receita no banco de dados com o status de "Rascunho", associada ao perfil do usuário. 
    11. **Sistema:** exibe a mensagem: "Receita salva como rascunho com sucesso!". 
* **Fluxos Alternativos:** Criação de Nova Tag. 
    * **FA1.** O texto digitado pelo usuário não corresponde a nenhuma tag existente na base de dados.
        1. **Sistema:** exibe uma opção clara, como: "Criar a tag '[texto digitado]'". 
        2. **Ator:** clica nesta opção. 
        3. **Sistema:** cria a nova tag no banco de dados, a adiciona à lista de tags da receita e a torna disponível para outros usuários no futuro. 
        4. Fluxo retorna ao **passo 7** do **Fluxo Principal**. 
* **Fluxos de Exceção:** 
    * **FE1** Um campo obrigatório não foi preenchido:  
        1. **Sistema:** destaca o campo em questão e exibe uma mensagem de erro, impedindo o salvamento.  

## Caso de uso 4 - Publicar receita 
* **Ator:** Usuário (autenticado). 
* **Resumo:** Usuário torna uma de suas receitas (previamente salva como rascunho) pública para que outros usuários possam visualizá-la e interagir com ela. 
* **Pré-condições:** 
    1. Usuário deve estar logado.   
    2. Usuário deve ter ao menos uma receita salva com o status “Rascunho”.  
* **Pós-condição:** A receita agora é pública e pode ser encontrada através da ferramenta de pesquisa.  
* **Fluxo Principal:**
    1. **Ator:** inicia o caso de uso acessando área "Minhas Receitas".
    2. **Ator:** seleciona a receita que deseja publicar. 
    3. **Ator:** na página da receita, clica no botão "Publicar". 
    4. **Sistema:** exibe uma mensagem de confirmação: "Deseja realmente tornar esta receita pública?". 
    5. **Ator:** confirma a ação. 
    6. **Sistema:** altera o status da receita de "Rascunho" para "Pública". 
    7. **Sistema:** exibe a mensagem: "Sua receita foi publicada com sucesso e já pode ser encontrada por outros usuários!". 

## Caso de uso 5 - Pesquisar receitas 
* **Ator:** Usuário (autenticado ou não). 
* **Resumo:** usuário busca por receitas públicas na plataforma, utilizando palavras-chave e filtros para refinar os resultados. 
* **Pré-condição:** Nenhuma. 
* **Pós-condição:** Nenhuma.  
* **Fluxo Principal:** 
    1. **Ator:** inicia o caso de uso acessando a página de busca. 
    2. **Ator:** digita um termo no campo de pesquisa (e.g., "bolo de fubá") e/ou aplica filtros como:
        * Ingredientes que deve conter. 
        * Ingredientes que NÃO deve conter. 
        * Tags específicas (e.g., "sem glúten", "festa junina"). 
    4. **Ator:** clica no botão "Pesquisar". 
    5. **Sistema:** busca no banco de dados todas as receitas públicas que correspondem aos critérios de busca. 
    6. **Sistema:** exibe uma lista de resultados, mostrando o título, a foto principal e a avaliação de cada receita encontrada. 
        -   Se não encontrar nenhuma receita, aciona o **FA1.**
* **Fluxos Alternativos:** 
    * **FA1.** Nenhuma receita é encontrada: 
        1. **Sistema:** exibe a mensagem: "Nenhuma receita encontrada. Tente usar outros termos ou filtros." 

## Caso de uso 6 - Comentar uma receita
* **Ator:** Usuário (autenticado). 
* **Resumo:** Usuário expressa sua opinião sobre uma receita pública, podendo deixar um comentário. 
* **Pré-condição:** 
    1. Usuário deve estar logado.  
    2. A receita visualizada deve ser pública.  
* **Pós-condição:** O comentário fica registrado e visível na página da receita.  
* **Fluxo Principal:** 
    1. **Ator:** abre a página de uma receita.
    2. **Ator:** rola a página até a seção de comentários. 
    3. **Ator:** digita seu comentário no campo de texto e clica em "Enviar". 
    4. **Sistema:** valida o comentário (e.g., não está vazio). 
    5. **Sistema:** salva o comentário e o exibe na lista de comentários da receita, junto com o nome do autor e a data. 
* **Fluxos de Exceção:** 
    * **FE1.** O comentário está vazio: 
        * **Sistema:** exibe a mensagem "O comentário não pode estar vazio." e não publica.  

## Caso de uso 7 - Curtir uma receita
* **Ator:** Usuário (autenticado). 
* **Resumo:** Usuário expressa sua opinião sobre uma receita pública, podendo curti-la ou deixar um comentário. 
* **Pré-condição:** 
    1. Usuário deve estar logado.  
    2. A receita visualizada deve ser pública. 
* **Pós-condição:** A curtida fica registrada e visível na página da receita. 
* **Fluxo Principal:** 
    1. **Ator:** abre a página de uma receita. 
    2. **Ator:** clica no botão "Curtir" (geralmente um ícone de coração). 
    3. **Sistema:** registra a curtida, associando-a ao usuário e à receita. 
    4. **Sistema:** o ícone de "Curtir" muda de estado (e.g., fica preenchido) e o contador de curtidas é incrementado. 
* **Fluxos Alternativos:** 
* **FA1.** Remover curtida:
    1. **Ator:** clica novamente no botão "Curtir".
    2. **Sistema:** o sistema remove a curtida (descurtir).  

## Caso de uso 8 - Alterar receita própria
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário modifica uma de suas receitas já criadas e o sistema automaticamente salva a versão anterior em um histórico, permitindo que ela seja consultada no futuro. 
* **Pré-condição:**
    1. Usuário deve estar logado 
    2. Usuário deve ser o autor da receita que deseja alterar. 
* **Pós-condição:** 
    1. Uma nova versão da receita é criada e se torna a versão atual.
    2. A versão anterior é salva no histórico da receita e pode ser consultada. 
* **Fluxo Principal:**: 
    1. **Ator:** acessa a sua área de "Minhas Receitas". 
    2. **Ator:** seleciona a receita que deseja modificar e clica na opção "Editar". 
    3. **Sistema:** exibe o formulário da receita preenchido com as informações da versão atual. 
    4. **Ator:** realiza as alterações desejadas. 
    5. **Ator:** clica no botão "Salvar Alterações". 
    6. **Sistema:** valida os dados. 
    7. **Sistema:** salva a versão anterior da receita em um histórico associado. 
    8. **Sistema:** define a nova versão como a "versão ativa" da receita. 
    9. **Sistema:** exibe a mensagem: "Receita atualizada com sucesso!".  
 
## Caso de uso  9 - Excluir e Anonimizar Receita Própria 
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário remove uma receita da visibilidade pública e desvincula seu nome de autoria dela permanentemente, sem prejudicar os usuários que a salvaram. 
* **Pré-condição:** usuário deve estar logado e ser o autor da receita. 
* **Pós-condição:** A receita não aparece mais em buscas ou no perfil do autor. Para usuários que a tinham salvado, ela aparecerá como uma contribuição anônima e poderá ser "adotada". 
* **Fluxo Principal:**: 
    1. **Ator:** acessa uma de suas receitas e clica na opção "Excluir". 
    2. **Sistema:** exibe uma caixa de diálogo de confirmação: "Você tem certeza que deseja excluir esta receita? Seu nome de usuário será removido dela, e a ação não poderá ser desfeita." 
    3. **Ator:** confirma a exclusão. 
    4. **Sistema:** altera o status da receita para "excluída_e_anônima". 
    5. **Sistema:** desvincula publicamente a receita do perfil do autor. 
    6. **Sistema:** exibe a mensagem: "Sua receita foi removida e não está mais visível publicamente." 

## Caso de uso 10 - Adaptar receita de outro Usuário
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário cria uma cópia de uma receita existente para seu próprio perfil, podendo então modificá-la livremente e publicá-la como sua, mas com uma atribuição à sua origem. 
* **Pré-condição:** **Ator:** deve estar logado. 
* **Pós-condição:** Uma nova receita em modo "Rascunho" é criada no perfil do usuário, pronta para ser editada e publicada. 
* **Fluxo Principal:**
    1. **Ator:** está visualizando a página de uma receita pública de outro usuário. 
    2. **Ator:** clica no botão "Adaptar esta Receita". 
    3. **Sistema:** cria uma cópia da receita e a salva no perfil do usuário atual 
    com o status "Rascunho". 
    4. **Sistema:** inclui uma menção automática à receita original (ex: "Baseada na receita '[Título Original]' de '[Autor Original]'").
    5. **Sistema:** redireciona o usuário para a tela de edição de sua nova 
    versão da receita. 
* **Fluxo Alternativo:** 
    * (Adotando Receita Anônima):
        1. **Ator:** está visualizando uma receita que consta em seus favoritos, mas que foi excluída e anonimizada pelo autor original. 
        2. **Ator:** clica no botão "Adotar esta Receita". 
        3. **Sistema:** cria uma cópia da receita e a salva no perfil do usuário atual com o status "Rascunho". 
        4. **Sistema:** adiciona um atributo especial à nova receita para indicar que sua origem é uma contribuição anônima. 
        5. **Sistema:** redireciona o usuário para a tela de edição. Ao ser publicada, esta receita exibirá a nota: "Esta receita foi adaptada de uma contribuição original da nossa comunidade."

## Caso de uso 11 - Remover comentário próprio 
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário apaga um comentário que ele mesmo fez em 
qualquer receita. 
* **Pré-condição:** usuário deve estar logado e ser o autor do comentário. 
* **Pós-condição:** O comentário é removido permanentemente da página da receita.
* **Fluxo Principal:**
    1. **Ator:** visualiza um comentário que deseja apagar e clica na opção "Excluir". 
    2. **Sistema:** exibe uma mensagem de confirmação: "Deseja mesmo excluir seu comentário?". 
    3. **Ator:** confirma. 
    4. **Sistema:** remove o comentário da lista de comentários da receita. 

## Caso de uso 12 -  Salvar receita em favoritos
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário adiciona uma receita pública a uma lista pessoal de "Favoritos" para encontrá-la facilmente mais tarde. 
* **Pré-condição:** usuário deve estar logado. 
* **Pós-condição:** A receita aparece na seção "Receitas Salvas" do perfil do usuário. 
* **Fluxo Principal:**: 
    1. **Ator:** está na página de uma receita que deseja salvar. 
    2. **Ator:** clica no botão "Salvar" ou em um ícone de "favorito". 
    3. **Sistema:** adiciona a receita à lista de "Receitas Salvas" do usuário. 
    4. **Sistema:** muda o ícone do botão de estado para indicar que a receita foi salva.  
* **Fluxo Alternativo:**
    * **FA1.** Remover dos salvos:
        1. **Ator:** clica novamente no botão "Salvar"
        2. **Sistema:** remove a receita da lista de favoritos do usuário. 

## Caso de uso 13 - Criar listas de receitas 
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário cria coleções personalizadas de receitas (ex: "Sobremesas de Natal") e adiciona receitas a essas listas. 
* **Pré-condição:** usuário deve estar logado. 
* **Pós-condição:** usuário pode visualizar suas listas e todas as receitas contidas nelas. 
* **Fluxo Principal:** 
    1. **Ator:** acessa a sua área de "Minhas Listas" e clica em "Criar Nova 
    Lista". 
    2. **Sistema:** solicita um nome para a lista. 
    3. **Ator:** insere o nome e confirma. 
    4. **Sistema:** cria uma lista vazia. 

## Caso de uso 14 - Adicionar recitas à lista
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário cria coleções personalizadas de receitas (ex: "Sobremesas de Natal") e adiciona receitas a essas listas. 
* **Pré-condição:** usuário deve estar logado. 
* **Pós-condição:** **Ator:** pode visualizar suas listas e todas as receitas contidas nelas. 
* **Fluxo Principal:** 
    1. Ao visualizar qualquer receita, usuário clica no botão "Adicionar à Lista". 
    2. **Sistema:** exibe as listas existentes do usuário.
    3. **Ator:** seleciona a lista onde deseja adicionar a receita. 
    4. **Sistema:** associa a receita à lista selecionada. 

## Caso de uso 15 - Visualizar histórico de versões da receita 
* **Ator:** Usuário (autenticado ou não). 
* **Resumo:** **Ator:** consulta as versões anteriores de uma receita que foi 
alterada pelo autor. 
* **Pré-condição:** A receita deve ter sido alterada pelo menos uma vez. 
* **Pós-condição:** **Ator:** consegue consultar o conteúdo exato de uma versão passada da receita.
* **Fluxo Principal:**: 
    1. **Ator:** está na página de uma receita e clica no link "Histórico de Alterações". 
    2. **Sistema:** exibe uma lista de todas as versões da receita, com a data de cada alteração. 
    3. **Ator:** clica em uma versão anterior para ver seus detalhes. 
    4. **Sistema:** exibe o conteúdo completo daquela versão, com um aviso claro de que se trata de uma versão antiga. 