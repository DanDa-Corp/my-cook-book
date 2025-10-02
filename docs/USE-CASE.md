# CASOS DE USO

## Caso de Uso 1 - Realizar cadastro de usuário
* **Ator:** Visitante (usuário não autenticado).
* **Resumo:** O visitante se cadastra na plataforma para se tornar um usuário, podendo criar e interagir com receitas.  
* **Pré-condições**: O visitante não pode ter uma conta existente com o e-mail fornecido.  
* **Pós-condição:** Uma nova conta de usuário é criada e o usuário está autenticado no sistema.  
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
* **Pré-condição:** usuário deve possuir uma conta ativa.  
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
* **Resumo:** Usuário cria receita, preenchendo todas as informações 
necessárias como título, ingredientes, modo de preparo e tags. 
* **Pré-condição:** **Ator:** deve estar logado no sistema. 
* **Pós-condição:** A receita é criada e armazenada no sistema, visível apenas para o usuário que a criou. 
* **Fluxo Principal:** (Caminho Feliz): 
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

## Caso de uso 6 - Comentar em uma receita
* **Ator:** Usuário. 
* **Resumo:** Usuário expressa sua opinião sobre uma receita pública, podendo deixar um comentário. 
* **Pré-condição:** 
    1. Usuário deve estar logado.  
    2. A receita visualizada deve ser pública. 
* **Pós-condição:** O comentário do Usuário fica registrada e visível na página da receita. 
* **Fluxo Principal:** 
    1. **Ator:** inicia o caso de uso abrindo uma receita. 
    4. **Ator:** rola a página até a seção de comentários. 
    5. **Ator:** digita seu comentário no campo de texto e clica em "Enviar". 
    6. **Sistema:** valida o comentário (e.g., não está vazio). 
    7. **Sistema:** salva o comentário e o exibe na lista de comentários da receita, junto com o nome do usuário e a data. 
* **Fluxos de Exceção:** 
    * **FE1.** O comentário está vazio: 
        1. **Sistema:** exibe a mensagem "O comentário não pode estar vazio." e não publica.  

## Caso de uso 7 - Curtir uma receita  
* **Ator:** Usuário. 
* **Resumo:** Usuário expressa sua opinião sobre uma receita pública, podendo deixar uma curtida. 
* **Pré-condição:** 
    1. Usuário deve estar logado.  
    2. A receita visualizada deve ser pública. 
* **Fluxo Principal:** 
    1. **Ator:** inicia o caso de uso abrindo uma receita.  
    2. **Ator:** clica no botão "Curtir" (geralmente um ícone de coração). 
    3. **Sistema:** registra a curtida, associando-a ao usuário e à receita. 
    4. **Sistema:** o ícone de "Curtir" muda de estado (e.g., fica preenchido) e o contador de curtidas é incrementado.
* **Fluxos Alternativos:** 
    * **FA1**: Clica novamente no botão "Curtir":
        1. **Sistema:** remove a curtida (descurtir). 

## Caso de uso 8 - Alterar receita própria
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário modifica uma de suas receitas já criadas. 
* **Pré-condição:** usuário deve estar logado e ser o autor da receita que deseja alterar. 
* **Pós-condição:** dados da receita estão alterados para futuras consultas.
* **Fluxo Principal:**: 
    1. **Ator:** acessa a sua área de "Minhas Receitas". 
    2. **Ator:** seleciona a receita que deseja modificar e clica na opção "Editar". 
    3. **Sistema:** exibe o formulário da receita preenchido com as informações da versão atual. 
    4. **Ator:** realiza as alterações desejadas. 
    5. **Ator:** clica no botão "Salvar Alterações". 
    6. **Sistema:** valida os dados e salva as alterações. 
    7. **Sistema:** exibe a mensagem: "Receita atualizada com sucesso!". 

## Caso de uso  9 - Excluir Receita Própria 
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário remove uma receita sua do sistema
* **Pré-condição:** usuário deve estar logado e ser o autor da receita. 
* **Pós-condição:** A receita não aparece mais em buscas ou no perfil do autor, não podendo consultá-la mais.
* **Fluxo Principal:**: 
    1. **Ator:** acessa uma de suas receitas e clica na opção "Excluir". 
    2. **Sistema:** exibe uma caixa de diálogo de confirmação: "Você tem     certeza que deseja excluir esta receita?" 
    3. **Ator:** confirma a exclusão. 
    4. **Sistema:** remove a receita do banco de dados.
    5. **Sistema:** exibe a mensagem: "Sua receita foi removida e não está mais visível publicamente." 

## Caso de uso 10 - Remover comentário próprio 
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário apaga um comentário que ele mesmo fez em qualquer receita. 
* **Pré-condição:** usuário deve estar logado e ser o autor do comentário. 
* **Pós-condição:** O comentário é removido permanentemente da página da receita. 
* **Fluxo Principal:**: 
    1. **Ator:** visualiza um comentário que deseja apagar e clica na opção     "Excluir". 
    2. **Sistema:** exibe uma mensagem de confirmação: "Deseja mesmo excluir seu comentário?". 
    3. **Ator:** confirma. 
    4. **Sistema:** remove o comentário da lista de comentários da receita. 

## Caso de uso 11 - Criar listas de receitas 
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário cria coleções personalizadas de receitas (ex: "Sobremesas de Natal").
* **Pré-condição:** usuário deve estar logado. 
* **Pós-condição:** usuário pode visualizar suas listas e todas as receitas contidas nelas. 
* **Fluxo Principal:** (Criar uma lista): 
    1. **Ator:** acessa a sua área de "Minhas Listas" e clica em "Criar Nova Lista". 
    2. **Sistema:** solicita um nome para a lista. 
    3. **Ator:** insere o nome e confirma. 
    4. **Sistema:** cria uma lista vazia. 

## Caso de uso 12 -  Salvar receita em lista
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário adiciona uma receita pública a uma lista pessoal para encontrá-la facilmente mais tarde. 
* **Pré-condição:** usuário deve estar logado.  
* **Pós-condição:** A receita aparece na lista selecionada pelo usuário. 
* **Fluxo Principal:**: 
    1. **Ator:** está na página de uma receita que deseja salvar. 
    2. **Ator:** clica no botão "Salvar". 
    3. **Sistema:** exibe uma tela com a mensagem "Deseja mesmo remover essa receita?"
    4. **Ator:** confirma a exclusão.
    5. **Sistema:** exibe uma tela de adição concluida.    

## Caso de uso 13 - Remover receita de uma lista
* **Ator:** Usuário (autenticado). 
* **Resumo:** usuário remove uma receita de uma lista pessoal. 
* **Pré-condição:** usuário deve estar logado.  
* **Pós-condição:** A receita não aparece na lista selecionada pelo usuário. 
* **Fluxo Principal:**: 
    1. **Ator:** está na página da lista que deseja remover uma receita.
    2. **Ator:** clica no botão em formato de lixeira
    3. **Sistema:** exibe uma tela com todas as listas criadas pelo usuário, para que escolha uma das listas.
    4. **Ator:** confirma a exclusão.
    5. **Sistema:** exibe uma tela de exclusão concluida.  
