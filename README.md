# code-refactor-digitaltok

-- CODE REFACTOR --

1. BookingRepository:

- database transaction must be used because multiple database create/update is done
- line:745 $current_translator -> we can use whereNull('cancel_at') instead
- line:746 could be -> if (!current_translator)
- line:747 could be -> whereNotNull('completed_at')
- line:1113 could be -> ($data['translator']) instead of ($data['translator'] != 0), because $data['translator'] != 0 means !=FALSE and 0 is considered to be "FALSE" in php.
- line:65 could be (->orderBy('due')) instead of (->orderBy('due', 'asc')), because orderBy is byDefault ASC
- each constant MUST be maintained in a separate file -> in case there is any change, we need to change it everywhere its used
- line:81 -> DB queries should NEVER be used in loops
- line:139 -> make a function "setResponse($fieldName)", because the code is repeating and only field_name is different
- line: 744 -> could be (!$current_translator) instead of (is_null($current_translator))
- line:1576 -> queries used in loop -> NEVER to do this

2. BookingController:

- must use try catch on each function
- line:38 could be -> ($request->used_id) instead of ($request->get('user_id')) because its the simpler format and input is also simple it's not nested or anything
- line:68 -> this line can be reduced by directly adding this ->  $this->repository->store($request->__authenticatedUser, $request->all())
- comments MUST be used to get better understanding of complex code / for new developers on project
