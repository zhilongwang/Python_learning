/* Injection point. Insert __afl_area_ptr load instruction, and insert 'nop' for future Binary Modification. */
        FunctionType * FTy = FunctionType::get(Type::getVoidTy(C), AFLMapPtr->getType(), false);
        InlineAsm *IA = InlineAsm::get(FTy,
          "mov $0,%rdi;nop;nop;nop;nop;nop;nop;nop;",
          "*m,~{rdi},~{cc},~{memory},~{dirflag},~{fpsr},~{flags}",
          true);
        CallInst *Result = IRB.CreateCall(IA, AFLMapPtr);
        Result->setMetadata(M.getMDKindID("nosanitize"), MDNode::get(C, None));
