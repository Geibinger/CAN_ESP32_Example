if(CONFIG_CAN_TARGET_SENDER)
    set(SRC "can_sender.c")
else()
    set(SRC "can_receiver.c")
endif()

idf_component_register(SRCS ${SRC}
                    INCLUDE_DIRS ".")
